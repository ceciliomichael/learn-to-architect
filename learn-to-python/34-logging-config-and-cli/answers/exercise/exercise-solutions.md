# Exercise Solutions: Logging, Configuration, and Command-Line Programs

```python
import argparse
import logging
import os
import sys
from pathlib import Path

logger = logging.getLogger(__name__)

def database_path_from_environment(allowed_directory: Path) -> Path:
    raw_path = os.environ.get("APP_DATABASE")
    if not raw_path:
        raise ValueError("APP_DATABASE is required")

    relative_path = Path(raw_path)
    if relative_path.is_absolute():
        raise ValueError("APP_DATABASE must be relative to the data directory")

    allowed_directory = allowed_directory.resolve()
    candidate = (allowed_directory / relative_path).resolve()
    if not candidate.is_relative_to(allowed_directory):
        raise ValueError("APP_DATABASE must stay inside the data directory")
    if candidate.suffix != ".db":
        raise ValueError("APP_DATABASE must end with .db")
    return candidate

def build_parser() -> argparse.ArgumentParser:
    parser = argparse.ArgumentParser(description="Read a practice file")
    parser.add_argument("path", type=Path)
    parser.add_argument("--limit", type=int, default=20)
    parser.add_argument("--verbose", action="store_true")
    return parser

def main(argv: list[str] | None = None) -> int:
    args = build_parser().parse_args(argv)
    logging.basicConfig(level=logging.DEBUG if args.verbose else logging.INFO)

    if args.limit < 1:
        print("limit must be positive", file=sys.stderr)
        return 2

    try:
        database_path = database_path_from_environment(Path.cwd() / "data")
    except ValueError as error:
        print(error, file=sys.stderr)
        return 2

    try:
        text = args.path.read_text(encoding="utf-8")
    except OSError:
        logger.exception("could not read requested input")
        return 1

    logger.info("using validated database file %s", database_path.name)
    print(text[: args.limit])
    return 0

if __name__ == "__main__":
    raise SystemExit(main())
```

Set `APP_DATABASE=practice.db` to select `data/practice.db`. The validator rejects absolute paths, parent traversal, and unexpected extensions before domain work begins. In a real application, authorization and operating-system permissions must also protect the allowed directory.

The CLI returns 2 for invalid arguments or configuration and 1 for a file operation failure. Its logs omit file contents, credentials, personal data, and the raw environment value.
