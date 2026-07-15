# Exercises: Async I/O with asyncio

1. Run three simulated I/O calls with TaskGroup and collect results.
2. Add a timeout shorter than one task and observe cancellation cleanup.
3. Limit ten tasks to two concurrent service sections with Semaphore.
4. Replace `time.sleep` with `asyncio.sleep` and compare responsiveness.
5. Move one blocking filesystem metadata call through `to_thread` and explain when this is useful.
