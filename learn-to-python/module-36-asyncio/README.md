# Module 36: Async I/O with asyncio

## What you will learn

You will run coroutines, manage task lifetimes, apply timeouts, handle cancellation, and keep blocking work off the event loop.

## Async cooperates at await points

```python
import asyncio

async def fetch_label(number: int) -> str:
    await asyncio.sleep(0.1)
    return f"item-{number}"

async def main() -> None:
    result = await fetch_label(1)
    print(result)

asyncio.run(main())
```

Calling an async function returns a coroutine object. `await` drives an awaitable and lets other tasks run while this task waits. Async does not make CPU-heavy code parallel.

Do not call `asyncio.run` from inside an already running event loop. Frameworks own their loop and provide an async entry point.

## Keep task lifetimes structured

Python 3.11 and newer provides TaskGroup:

```python
async def main() -> None:
    async with asyncio.TaskGroup() as group:
        tasks = [group.create_task(fetch_label(i)) for i in range(3)]
    print([task.result() for task in tasks])
```

The context waits for all tasks. If one fails, remaining tasks are cancelled and failures are reported as an exception group. Keep references to created tasks and always observe their completion.

`asyncio.gather` is useful for ordered aggregate results but has different failure and cancellation behavior. Read its contract instead of treating it as interchangeable with TaskGroup.

## Bound waiting and concurrency

```python
async def fetch_with_timeout() -> str:
    async with asyncio.timeout(2.0):
        return await fetch_label(1)
```

Timeout cancels the work through task cancellation. Code should use `try/finally` for cleanup and normally re-raise `asyncio.CancelledError` after cleanup.

Use a semaphore to limit access to a scarce service:

```python
limit = asyncio.Semaphore(10)

async def limited_fetch(number: int) -> str:
    async with limit:
        return await fetch_label(number)
```

Concurrency limits, service timeouts, and retry policies prevent overwhelming dependencies.

## Do not block the event loop

Ordinary file calls, CPU loops, `time.sleep`, and blocking libraries stop all tasks on that event-loop thread. Use async-capable libraries, `await asyncio.sleep`, or move a short blocking call to a thread:

```python
from pathlib import Path

async def file_size(path: Path) -> int:
    information = await asyncio.to_thread(path.stat)
    return information.st_size
```

This does not turn CPU-heavy Python into process parallelism.

## Async resources need async contexts

Use `async with` for sessions, connections, locks, and other async managers. Use `async for` for asynchronous iterators. Close the resource before the loop shuts down.

## Check your understanding

You are ready when you can identify every yield point, contain task lifetimes, and explain how cancellation reaches cleanup.
