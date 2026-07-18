# Module 38: Project Structure, Packaging, and Secure Boundaries

## What you will learn

You will organize a distributable project, define a small public API, load resources safely, and defend process and data boundaries.

## Use a source layout

```text
clearcourse-tools/
  pyproject.toml
  README.md
  src/
    clearcourse_tools/
      __init__.py
      cli.py
      service.py
  tests/
    test_service.py
```

The source layout prevents the project root from accidentally satisfying imports during tests. Install the package into the environment, often in editable mode during development:

```text
python -m pip install --editable .
```

## Declare project metadata

One complete setuptools-based `pyproject.toml` is:

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
```

The build backend is a dependency and trust decision. Pinning policy, lock files, build isolation, artifact signing, and publishing credentials follow the team's release process.

## Keep a small public API

`__init__.py` can re-export supported names:

```python
from .service import normalize_title

__all__ = ["normalize_title"]
```

Document compatibility for public names. A leading underscore marks implementation details by convention. Semantic versioning communicates intent but does not replace tests and release notes.

## Load packaged resources

Do not assume resources are ordinary files beside `__file__`. Use `importlib.resources`:

```python
from importlib.resources import files

template = files("clearcourse_tools").joinpath("default.txt").read_text(
    encoding="utf-8"
)
```

Configure the build backend to include required resource files and test the built wheel, not only the source tree.

## Validate every external boundary

Boundaries include CLI arguments, environment variables, files, JSON, databases, HTTP responses, plugin code, and message queues. Parse into a small validated domain object before core logic. Enforce size, type, range, authorization, and allowed-value rules.

Never deserialize untrusted pickle data. Pickle can execute arbitrary code while loading. JSON is safer as data syntax but still needs size and schema validation.

## Run subprocesses without shell injection

```python
import subprocess

result = subprocess.run(
    ["python", "--version"],
    check=True,
    capture_output=True,
    text=True,
    timeout=10,
)
```

Pass an argument list and keep `shell=False`, the default. Do not build a shell command from untrusted text. Use absolute or controlled executable paths when path substitution is a threat. Bound time and output, set a minimal environment, and apply operating-system permissions.

## Separate responsibilities without excess layers

A maintainable small application often separates:

- Entry adapters that parse and report
- Domain functions that enforce meaning
- I/O adapters for files, databases, or services
- Configuration assembled at startup

Add a boundary when it protects a real responsibility or improves testing. Do not create layers only to look advanced.

## Release from verified artifacts

1. Create a clean environment.
2. Run formatting, static checks, tests, and security review.
3. Build source and wheel artifacts with the approved backend.
4. Install the wheel in another clean environment.
5. Test imports, CLI entry, resources, metadata, and supported Python versions.
6. Generate provenance and publish through protected credentials.
7. Monitor and retain a rollback or corrected-release plan.

## Check your understanding

You are ready when you can explain the source layout, validate boundaries before domain logic, and test the exact artifact that users install.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
