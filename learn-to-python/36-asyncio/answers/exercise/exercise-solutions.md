# Exercise Solutions: Async I/O with asyncio

```python
import asyncio
from pathlib import Path

async def simulated_call(
    number: int,
    limit: asyncio.Semaphore,
    activity: dict[str, int],
) -> str:
    async with limit:
        activity["current"] += 1
        activity["maximum"] = max(activity["maximum"], activity["current"])
        try:
            await asyncio.sleep(0.1)
            return f"result-{number}"
        finally:
            activity["current"] -= 1
            print(f"finished {number}")

async def run_group(count: int, timeout_seconds: float) -> list[str]:
    limit = asyncio.Semaphore(2)
    activity = {"current": 0, "maximum": 0}
    tasks: list[asyncio.Task[str]] = []
    async with asyncio.timeout(timeout_seconds):
        async with asyncio.TaskGroup() as group:
            tasks = [
                group.create_task(simulated_call(number, limit, activity))
                for number in range(count)
            ]
    print("maximum service concurrency:", activity["maximum"])
    return [task.result() for task in tasks]

async def main() -> None:
    print(await run_group(3, 2.0))

    try:
        await run_group(3, 0.05)
    except TimeoutError:
        print("timed out after cancellation cleanup")

    print(await run_group(10, 2.0))

    size = await asyncio.to_thread(Path(__file__).stat)
    print("current file bytes:", size.st_size)

if __name__ == "__main__":
    asyncio.run(main())
```

The first group completes three calls. The short timeout cancels its tasks, but every `finally` block still runs before `TimeoutError` is handled. The ten-task run reports a maximum of two active service sections because the semaphore guards that section.

`asyncio.to_thread` keeps the small blocking metadata call off the event-loop thread. It is useful when a blocking library has no async API and the work is brief or I/O-oriented. It does not make CPU-heavy Python run in process-level parallel.

Replace any `time.sleep(0.1)` inside a coroutine with `await asyncio.sleep(0.1)`. The ordinary sleep blocks every task on that event-loop thread, while the awaited sleep lets other ready tasks progress.
