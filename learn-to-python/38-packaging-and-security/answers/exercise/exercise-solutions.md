# Exercise Solutions: Project Structure, Packaging, and Secure Boundaries

Create this project:

```text
clearcourse-tools/
  pyproject.toml
  README.md
  src/
    clearcourse_tools/
      __init__.py
      cli.py
      default.txt
      resources.py
      service.py
  tests/
    test_service.py
```

`pyproject.toml`:

```toml
[build-system]
requires = ["setuptools>=68"]
build-backend = "setuptools.build_meta"

[project]
name = "clearcourse-tools"
version = "0.1.0"
description = "Small learning utilities"
readme = "README.md"
requires-python = ">=3.12"
dependencies = []

[project.scripts]
clearcourse = "clearcourse_tools.cli:main"

[tool.setuptools.packages.find]
where = ["src"]

[tool.setuptools.package-data]
clearcourse_tools = ["default.txt"]
```

`README.md`:

```markdown
# Clearcourse Tools

A small package for practicing validated Python command-line tools.
```

`src/clearcourse_tools/service.py`:

```python
from typing import Literal

Mode = Literal["title", "lower"]

def normalize_title(text: str, mode: Mode = "title") -> str:
    cleaned = " ".join(text.split())
    if not cleaned:
        raise ValueError("title is required")
    if len(cleaned) > 200:
        raise ValueError("title is too long")
    if mode == "title":
        return cleaned.title()
    if mode == "lower":
        return cleaned.casefold()
    raise ValueError("mode must be title or lower")
```

`src/clearcourse_tools/resources.py`:

```python
from importlib.resources import files

def default_message() -> str:
    return files("clearcourse_tools").joinpath("default.txt").read_text(
        encoding="utf-8"
    ).strip()
```

Put `Welcome to Clearcourse.` in `src/clearcourse_tools/default.txt`.

`src/clearcourse_tools/__init__.py`:

```python
from .resources import default_message
from .service import Mode, normalize_title

__all__ = ["Mode", "default_message", "normalize_title"]
```

`src/clearcourse_tools/cli.py`:

```python
import argparse
import subprocess
import sys

from .service import normalize_title

def runtime_version() -> str:
    result = subprocess.run(
        [sys.executable, "--version"],
        check=True,
        capture_output=True,
        text=True,
        timeout=10,
        shell=False,
    )
    return (result.stdout or result.stderr).strip()

def main(argv: list[str] | None = None) -> int:
    parser = argparse.ArgumentParser()
    parser.add_argument("title")
    parser.add_argument("--mode", choices=("title", "lower"), default="title")
    parser.add_argument("--show-python", action="store_true")
    args = parser.parse_args(argv)
    try:
        print(normalize_title(args.title, args.mode))
    except ValueError as error:
        parser.error(str(error))
    if args.show_python:
        print(runtime_version())
    return 0
```

`tests/test_service.py`:

```python
import unittest

from clearcourse_tools import default_message, normalize_title

class ServiceTests(unittest.TestCase):
    def test_normalizes_supported_modes(self) -> None:
        self.assertEqual(normalize_title("  clear   python  "), "Clear Python")
        self.assertEqual(normalize_title("  Clear   Python  ", "lower"), "clear python")

    def test_rejects_empty_and_oversized_text(self) -> None:
        with self.assertRaisesRegex(ValueError, "required"):
            normalize_title("   ")
        with self.assertRaisesRegex(ValueError, "too long"):
            normalize_title("x" * 201)

    def test_loads_packaged_resource(self) -> None:
        self.assertEqual(default_message(), "Welcome to Clearcourse.")
```

The `choices` argument rejects unsupported modes at the CLI boundary. The domain function repeats the allowed-value check because it can also be called without the CLI. Length and empty-value rules run before normalization is returned.

The subprocess uses a fixed executable and fixed argument, keeps `shell=False`, and has a timeout. Joining untrusted text into shell syntax would let shell operators change the command, so this package does not accept shell command text.

In PowerShell, install and test the editable project:

```text
python -m venv .venv
.\.venv\Scripts\python -m pip install --editable .
.\.venv\Scripts\python -m unittest discover -s tests -v
.\.venv\Scripts\clearcourse "  Clear   Python  " --mode lower --show-python
```

Use your team's approved and reviewed build frontend. If that frontend is `build`, create and verify a wheel with:

```text
.\.venv\Scripts\python -m pip install build
.\.venv\Scripts\python -m build
python -m venv .venv-wheel
.\.venv-wheel\Scripts\python -m pip install dist\clearcourse_tools-0.1.0-py3-none-any.whl
.\.venv-wheel\Scripts\python -m unittest discover -s tests -v
.\.venv-wheel\Scripts\clearcourse "Wheel test" --show-python
```

On POSIX systems, use `.venv/bin/python` and `.venv-wheel/bin/python`. Testing with the wheel environment proves that imports, the CLI entry point, and packaged resource work from the artifact users receive, not only from the source tree.
