# Running the `getflags` examples with `uv`

This directory contains the `flags*`, `flags2*`, `flags3*`, and `flags4*` examples
from Fluent Python 2e. Dependencies (`httpx`, `tqdm`) are managed at the repo root
in [pyproject.toml](../../pyproject.toml), so `uv run` from this directory picks
them up automatically.

## Prerequisites

- `uv` installed (https://docs.astral.sh/uv/)
- From the repo root, dependencies sync on first `uv run`. To pre-sync:

  ```sh
  uv sync
  ```

- Unzip `flags.zip` so the test server has files to serve:

  ```sh
  unzip flags.zip
  ```

  This creates `flags/` with subdirectories `ad/` … `zw/`.

## Running `flags4_asyncio_taskgroup.py`

`flags4` is the `asyncio.TaskGroup` variant of the error-handling client. It
accepts the same CLI as the other `flags2*`/`flags3*` scripts. View the options:

```sh
uv run flags4_asyncio_taskgroup.py -h
```

The most important flag is `-s/--server`, which selects the base URL:

| Label    | URL                                  | Server to start                                         |
|----------|--------------------------------------|---------------------------------------------------------|
| `LOCAL`  | `http://localhost:8000/flags`        | `python -m http.server` (port 8000)                     |
| `DELAY`  | `http://localhost:8001/flags`        | `slow_server.py` on port 8001                           |
| `ERROR` | `http://localhost:8002/flags`        | `slow_server.py 8002 --error-rate .25`                  |
| `REMOTE` | `http://fluentpython.com/data/flags` | none — public server, be gentle                         |

### Start the servers

Each server runs in its own terminal, from this directory.

**LOCAL** — plain static file server on port 8000:

```sh
uv run python -m http.server
```

**DELAY** — adds a random 0.5s–5s delay to every response, port 8001:

```sh
uv run slow_server.py
```

**ERROR** — 25% chance of HTTP 418, every response delayed 0.5s, port 8002:

```sh
uv run slow_server.py 8002 --error-rate .25
```

Verify a server is up by opening http://localhost:8000/flags/ in a browser — you
should see country-code directories from `ad/` to `zw/`.

### Run the client

In a separate terminal:

```sh
# default: 20 most populous countries, LOCAL server
uv run flags4_asyncio_taskgroup.py

# hit the delay server with 50 concurrent requests, verbose
uv run flags4_asyncio_taskgroup.py -s DELAY -m 50 -v

# hit the error server, all flags
uv run flags4_asyncio_taskgroup.py -s ERROR -a

# specific country codes
uv run flags4_asyncio_taskgroup.py BR CN DE
```

Downloaded flags land in `downloaded/` (gitignored).

## Other clients in this directory

All accept the same CLI and can be run the same way:

- [flags2_sequential.py](flags2_sequential.py) — one request at a time
- [flags2_threadpool.py](flags2_threadpool.py) — `concurrent.futures.ThreadPoolExecutor`
- [flags2_asyncio.py](flags2_asyncio.py) — `asyncio.as_completed`
- [flags2_asyncio_executor.py](flags2_asyncio_executor.py) — `asyncio` + executor for the file write
- [flags3_asyncio.py](flags3_asyncio.py) — adds the second request per country (`metadata.json`)
- [flags4_asyncio_taskgroup.py](flags4_asyncio_taskgroup.py) — `flags3` rewritten with `asyncio.TaskGroup`

The simpler `flags.py`, `flags_asyncio.py`, `flags_threadpool.py`, and
`flags_threadpool_futures.py` scripts have no `-s` option and always use
`http://localhost:8000/flags` (the `LOCAL` server above).

## macOS SSL certificates

If `REMOTE` fails with an SSL error, install Python's CA bundle by running
`Install Certificates.command` from your `/Applications/Python 3.X/` folder. Not
needed when hitting only the local servers.
