# Mojifinder: Unicode character search examples

Examples from _Fluent Python, Second Edition_—Chapter 22, _Asynchronous Programming_.

## How to run `web_mojifinder.py`

`web_mojifinder.py` is a Web application built with _[FastAPI](https://fastapi.tiangolo.com/)_.
It was tested with the _[Uvicorn](https://www.uvicorn.org/)_ ASGI server.

Both `fastapi` and `uvicorn` are declared in the project's `pyproject.toml` at the
repo root, so [uv](https://docs.astral.sh/uv/) will install them automatically.

From this directory:

```
$ uv run uvicorn web_mojifinder:app
```

Or from the repo root:

```
$ uv run --directory 21-async/mojifinder uvicorn web_mojifinder:app
```

Finally, visit http://127.0.0.1:8000/ with your browser to see the search form.

## How to run `web_mojifinder_bottle.py`

This variant uses the bundled `bottle.py` (no extra install needed) and runs as a script:

```
$ uv run python web_mojifinder_bottle.py
```

## How to run `tcp_mojifinder.py`

Standard library only — run it directly:

```
$ uv run python tcp_mojifinder.py
```


## Directory contents

These files can be run as scripts directly from the command line:

- `charindex.py`: libray used by the Mojifinder examples. Also works as CLI search script.
- `tcp_mojifinder.py`: TCP/IP Unicode search server. Depends only on the Python 3.9 standard library. Use a telnet application as client.
- `web_mojifinder_bottle.py`: Unicode Web service. Depends on `bottle.py` and `static/form.html`. Use an HTTP browser as client.

This program requires an ASGI server to run it:

- `web_mojifinder.py`: Unicode Web service. Depends on _[FastAPI](https://fastapi.tiangolo.com/)_ and `static/form.html`.

Support files:

- `bottle.py`: local copy of the single-file _[Bottle](https://bottlepy.org/)_ Web framework.
- `requirements.txt`: list of dependencies for `web_mojifinder.py`.
- `static/form.html`: HTML form used by the `web_*` examples.
- `README.md`: this file 🤓
