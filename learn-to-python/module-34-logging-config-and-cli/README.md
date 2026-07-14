# Module 34: Logging, Configuration, and Command-Line Programs

## What you will learn

You will report operational events, validate configuration, parse command arguments, and return meaningful exit codes.

## Logging has an audience and level

```python
import logging

logger = logging.getLogger(__name__)

def process_order(order_id: int) -> None:
    logger.info("processing order", extra={"order_id": order_id})
```

Libraries should create named loggers and not configure global handlers at import time. The application entry point configures logging:

```python
logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s %(levelname)s %(name)s %(message)s",
)
```

Use debug for diagnostic detail, info for normal meaningful events, warning for recoverable concerns, error for failed operations, and critical for severe system-wide failure. Do not log every loop iteration by default.

## Never log secrets or unnecessary personal data

Passwords, tokens, authorization headers, connection strings, and sensitive records must be redacted or omitted. Logging arguments lazily is efficient:

```python
logger.info("processed order %s", order_id)
```

Use `logger.exception("message")` inside an exception handler to include the traceback. User-facing output should remain concise and should not expose internal paths or secrets.

## Read and validate configuration

```python
import os

database_path = os.environ.get("APP_DATABASE")
if not database_path:
    raise RuntimeError("APP_DATABASE is required")
```

Environment variables are strings. Convert and validate types, ranges, allowed values, and paths at startup. Environment variables are not automatically secret: child processes, diagnostics, or deployment tools may expose them. Use the platform's approved secret mechanism.

## Parse a command line with argparse

```python
import argparse

def build_parser() -> argparse.ArgumentParser:
    parser = argparse.ArgumentParser(description="List products")
    parser.add_argument("--limit", type=int, default=20)
    parser.add_argument("--active", action="store_true")
    return parser
```

Keep parsing at the program edge. Pass ordinary values into application functions.

## Return exit codes

```python
def main(argv: list[str] | None = None) -> int:
    args = build_parser().parse_args(argv)
    if args.limit < 1:
        print("limit must be positive", file=sys.stderr)
        return 2
    return 0

if __name__ == "__main__":
    raise SystemExit(main())
```

Exit code zero means success. Nonzero means failure, with conventions documented for automation. Normal result output goes to stdout; diagnostics go to stderr.

## Check your understanding

You are ready when you can separate logs, user output, configuration validation, command parsing, and process exit status.
