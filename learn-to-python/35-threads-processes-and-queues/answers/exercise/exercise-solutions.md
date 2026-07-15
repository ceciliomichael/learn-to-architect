# Exercise Solutions: Threads, Processes, and Queues

```python
from concurrent.futures import ProcessPoolExecutor, ThreadPoolExecutor
from pathlib import Path
from queue import Queue
from tempfile import TemporaryDirectory
from threading import Lock, Thread
from time import perf_counter, sleep

def file_size(path: Path) -> tuple[str, int]:
    return path.name, path.stat().st_size

def square(value: int) -> int:
    return value * value

def timed(function, *args):
    start = perf_counter()
    result = function(*args)
    return result, perf_counter() - start

def read_all_sequential(paths: list[Path]) -> list[tuple[str, int]]:
    return [file_size(path) for path in paths]

def read_all_threaded(paths: list[Path]) -> list[tuple[str, int]]:
    with ThreadPoolExecutor(max_workers=2) as executor:
        futures = [executor.submit(file_size, path) for path in paths]
        return [future.result() for future in futures]

def demonstrate_counter() -> None:
    unsafe_total = 0

    def unsafe_increment() -> None:
        nonlocal unsafe_total
        for _ in range(500):
            current = unsafe_total
            sleep(0)
            unsafe_total = current + 1

    threads = [Thread(target=unsafe_increment) for _ in range(4)]
    for thread in threads:
        thread.start()
    for thread in threads:
        thread.join()
    print("unsafe total:", unsafe_total, "expected:", 2000)

    safe_total = 0
    lock = Lock()

    def safe_increment() -> None:
        nonlocal safe_total
        for _ in range(500):
            with lock:
                safe_total += 1

    threads = [Thread(target=safe_increment) for _ in range(4)]
    for thread in threads:
        thread.start()
    for thread in threads:
        thread.join()
    print("locked total:", safe_total)

def demonstrate_queue() -> None:
    sentinel = object()
    messages: Queue[object] = Queue()

    def consume() -> None:
        while True:
            item = messages.get()
            try:
                if item is sentinel:
                    return
                print("consumed:", item)
            finally:
                messages.task_done()

    consumer = Thread(target=consume)
    consumer.start()
    for number in range(3):
        messages.put(number)
    messages.put(sentinel)
    messages.join()
    consumer.join()

def main() -> None:
    with TemporaryDirectory() as directory:
        root = Path(directory)
        paths = []
        for number in range(4):
            path = root / f"thread-{number}.txt"
            path.write_text("x" * (number + 1), encoding="utf-8")
            paths.append(path)

        sequential, sequential_time = timed(read_all_sequential, paths)
        threaded, threaded_time = timed(read_all_threaded, paths)
        print(sequential)
        print(threaded)
        print("read seconds:", sequential_time, threaded_time)

    demonstrate_counter()
    demonstrate_queue()

    with ProcessPoolExecutor() as executor:
        print(list(executor.map(square, range(10))))

if __name__ == "__main__":
    main()
```

The forced yield makes lost counter updates easy to observe, but race outcomes are not guaranteed. The lock makes the compound update one protected operation. For real calculations, having each worker return a value and letting the main thread call `sum` is often clearer than sharing a counter.

The queue consumer calls `task_done` in `finally`, including for the sentinel, so `join` cannot wait forever after normal handling. The process code stays behind the main guard for Windows and other spawn-based systems.

The printed timings are evidence for only this machine, workload, and run. Tiny local files may make threads slower. Repeat with representative I/O before choosing a design, and never claim that concurrency is faster merely because it uses more workers.
