# poetry-bug

A bug in how Poetry 1.4.0+ interacts with mypy and local packages. To reproduce
the bug, perform the following steps:

```bash
$ git clone https://github.com/RyanGlScott/poetry-bug
$ cd poetry-bug/bar

# First, try Poetry 1.3.2, which is known to work
$ poetry self update 1.3.2
$ rm -rf ~/.cache/pypoetry/ .mypy_cache && poetry update && poetry install
$ poetry run mypy --install-types --non-interactive bar/
Success: no issues found in 1 source file

$ # Next, try Poetry 1.4.2, which fails
$ poetry self update 1.4.2
$ rm -rf ~/.cache/pypoetry/ .mypy_cache && poetry update && poetry install
$ poetry run mypy --install-types --non-interactive bar/
bar/__init__.py:1: error: Cannot find implementation or library stub for module named "foo"  [import]
bar/__init__.py:1: note: See https://mypy.readthedocs.io/en/stable/running_mypy.html#missing-imports
Found 1 error in 1 file (checked 1 source file)
```
