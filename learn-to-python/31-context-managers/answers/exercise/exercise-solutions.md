# Exercise Solutions: Context Managers

```python
from contextlib import ExitStack, contextmanager
from pathlib import Path
from tempfile import TemporaryDirectory
from time import perf_counter

class Announce:
    def __enter__(self):
        print("Starting")
        return self

    def __exit__(self, exception_type, exception, traceback):
        print("Finishing")
        return False

try:
    with Announce():
        raise RuntimeError("practice failure")
except RuntimeError as error:
    print(f"Propagated: {error}")

@contextmanager
def timer():
    start = perf_counter()
    try:
        yield
    finally:
        print(f"Elapsed: {perf_counter() - start:.6f}")

with timer():
    sum(range(10_000))

with TemporaryDirectory() as directory:
    paths = [Path(directory) / "one.txt", Path(directory) / "two.txt"]
    for path in paths:
        path.write_text(path.stem, encoding="utf-8")
    with ExitStack() as stack:
        files = [stack.enter_context(path.open(encoding="utf-8")) for path in paths]
        print([file.read() for file in files])

class ExpectedPracticeError(Exception):
    pass

class SuppressExpected:
    def __enter__(self):
        return self

    def __exit__(self, exception_type, exception, traceback):
        return exception_type is ExpectedPracticeError

with SuppressExpected():
    raise ExpectedPracticeError("handled by policy")

try:
    with SuppressExpected():
        raise ValueError("must propagate")
except ValueError as error:
    print(error)
```

Announce prints its finish message and returns false, so the block exception continues outward. SuppressExpected returns true only for its documented custom exception. A different exception still propagates.

Other suitable resources include a thread lock, a database transaction, and a temporary directory. Each has a clear acquire-use-release lifetime even though no ordinary file is involved.
