# Module 31: Context Managers

## What you will learn

You will guarantee paired setup and cleanup and manage dynamic groups of resources.

## With defines a managed region

```python
with open("notes.txt", "r", encoding="utf-8") as file:
    text = file.read()
```

Python calls the context manager's `__enter__`, binds its result after `as`, runs the block, then calls `__exit__` even when the block raises.

## Build a class-based manager

```python
class Announce:
    def __enter__(self):
        print("Starting")
        return self

    def __exit__(self, exception_type, exception, traceback):
        print("Finishing")
        return False
```

Returning false or `None` lets an exception continue. Returning true suppresses it. Suppress only a narrowly documented expected exception; silent suppression hides failures.

Cleanup code in `__exit__` must handle partially completed work and should not replace the original exception with an avoidable cleanup error.

## Use contextmanager for simple generators

```python
from contextlib import contextmanager

@contextmanager
def managed_message():
    print("Starting")
    try:
        yield "ready"
    finally:
        print("Finishing")
```

The function must yield exactly once. Work before yield is entry; finalization after it is exit.

## Manage a dynamic number with ExitStack

```python
from contextlib import ExitStack

paths = ["one.txt", "two.txt"]
with ExitStack() as stack:
    files = [
        stack.enter_context(open(path, "r", encoding="utf-8"))
        for path in paths
    ]
    contents = [file.read() for file in files]
```

If opening a later file fails, ExitStack closes earlier files. It also registers callbacks and supports transferring a cleanup stack when ownership changes.

## Context managers are not only files

They manage locks, database transactions, temporary directories, decimal contexts, and network sessions. The common idea is a reliable lifetime around a block.

Async context managers use `async with` and `__aenter__` or `__aexit__`, taught after async fundamentals.

## Check your understanding

You are ready when you can explain entry, block, exit, propagation, and why ExitStack helps partial acquisition.
