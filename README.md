# Fluent Python 2e example code

Example code for the book **Fluent Python, Second Edition** by Luciano Ramalho (O'Reilly, 2022).


## Running the code with [uv](https://docs.astral.sh/uv/)

This repository ships with a `pyproject.toml` and `uv.lock` so a single shared environment covers the example code across chapters. Python 3.12 is pinned via `.python-version`.

### One-time setup

```sh
uv sync
```

That installs the runtime deps (`click`, `fastapi`, `geolib`, `httpx`, `tqdm`, `uvicorn`) plus the dev tools (`pytest`, `mypy`, `ruff`) into `.venv/`.

### Running scripts

Use `uv run` — no need to activate the venv:

```sh
uv run python 19-concurrency/spinner_thread.py
uv run python 20-executors/demo_executor_map.py
```

### Running doctests

`pytest.ini` is configured with `--doctest-modules`, so most chapter files double as doctests:

```sh
uv run pytest 11-pythonic-obj/vector2d_v0.py
uv run pytest 17-it-generator/sentence.py
```

### Type-checking and linting

```sh
uv run mypy 11-pythonic-obj/vector2d_v0.py
uv run ruff check 11-pythonic-obj/
```

### Caveats

- **`curio`** (used only in [21-async/domains/curio](21-async/domains/curio)) is *not* in the shared env — its latest release is broken on Python 3.12. To run that example, create a separate environment with Python ≤3.11:
  ```sh
  cd 21-async/domains/curio && uv venv --python 3.11 && uv pip install curio
  ```
- A few chapters have their own `requirements.txt` from the upstream book repo. They overlap with the root environment and can generally be ignored.


## Table of Contents

All chapters are undergoing review and updates, including significant rewrites in the chapters about concurrency in **Part V**.

New chapters in **Fluent Python 2e** are marked with 🆕.

> 🚨 &nbsp;This table of contents is subject to change at any time until the book goes to the printer.<BR>
Latest change: Old **Part I—Prologue** merged into new **Part I—Data Structures**; parts renumbered accordingly; chapter numbers unchanged.

Part / Chapter #|Title|Directory|1<sup>st</sup> ed. Chapter&nbsp;#
---:|---|---|:---:
**I – Data Structures**|
1|The Python Data Model|[01-data-model](01-data-model)|1
2|An Array of Sequences|[02-array-seq](02-array-seq)|2
3|Dictionaries and Sets|[03-dict-set](03-dict-set)|3
4|Unicode Text versus Bytes|[04-text-byte](04-text-byte)|4
5|Data Class Builders|[05-data-classes](05-data-classes)|🆕
6|Object References, Mutability, and Recycling|[06-obj-ref](06-obj-ref)|8
**II – Functions as Objects**|
7|Funcions as First-Class Objects|[07-1class-func](07-1class-func)|5
8|Type Hints in Functions|[08-def-type-hints](08-def-type-hints)|🆕
9|Decorators and Closures|[09-closure-deco](09-closure-deco)|7
10|Design Patterns with First-Class Functions|[10-dp-1class-func](10-dp-1class-func)|6
**III – Object-Oriented Idioms**|
11|A Pythonic Object|[11-pythonic-obj](11-pythonic-obj)|9
12|Special Methods for Sequences|[12-seq-hacking](12-seq-hacking)|10
13|Interfaces, Protocols, and ABCs|[13-protocl-abc](13-protocol-abc)|11
14|Inheritance: For Better or For Worse|[14-inheritance](14-inheritance)|12
15|More About Type Hints|[15-more-types](15-more-types)|🆕
16|Operator Overloading|[16-op-overloading](16-op-overloading)|13
**IV – Control Flow**|
17|Iterators, Generators, and Classic Coroutines|[17-it-generator](17-it-generator)|14
18|with, match, and else Blocks|[18-with-match](18-with-match)|15
19|Concurrency Models in Python|[19-concurrency](19-concurrency)|🆕
20|Concurrent Executors|[20-executors](20-executors)|17
21|Asynchronous Programming|[21-async](21-async)|18
**V – Metaprogramming**|
22|Dynamic Attributes and Properties|[22-dyn-attr-prop](22-dyn-attr-prop)|19
23|Attribute Descriptors|[23-descriptor](23-descriptor)|20
24|Class Metaprogramming|[24-class-metaprog](24-class-metaprog)|21
