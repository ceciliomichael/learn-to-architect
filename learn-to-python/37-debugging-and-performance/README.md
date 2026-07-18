# Module 37: Debug, Profile, and Improve Performance

## What you will learn

You will reproduce failures, inspect state, measure bottlenecks, and improve algorithms before micro-optimizing syntax.

## Debug from evidence

1. Reproduce the smallest reliable failure.
2. Read the entire traceback.
3. State expected and actual behavior.
4. Inspect inputs and state near the first wrong value.
5. Form one hypothesis.
6. Change one cause and rerun tests.

Use `breakpoint()` to enter the debugger:

```python
def total(values):
    breakpoint()
    return sum(values)
```

Useful debugger commands include `n` for next line, `s` for step into, `p expression` to inspect, `l` to list source, `c` to continue, and `q` to quit. Remove accidental breakpoints before release.

## Assertions are developer checks

```python
assert total >= 0, "total invariant failed"
```

Assertions can be disabled with optimization and should not validate user input, permissions, payments, or other required runtime boundaries. Raise explicit exceptions there.

## Measure before optimizing

`time.perf_counter` measures elapsed durations. `timeit` repeats small snippets with setup control. `cProfile` reports function call time:

```text
python -m cProfile -s cumulative app.py
```

Profile a representative workload. Debug mode, warm caches, background activity, data size, and I/O all affect results.

## Algorithmic growth matters

Membership in a list usually scans items, while set membership is usually constant average time. A nested full scan can grow roughly with the product of input sizes. Choose the correct data structure and algorithm before shaving tiny syntax costs.

Complexity describes growth, not actual milliseconds. Measure constants and real distributions too.

## Cache only safe functions

```python
from functools import lru_cache

@lru_cache(maxsize=256)
def parse_code(code: str) -> tuple[str, str]:
    return tuple(code.split(":", maxsplit=1))
```

Cache functions whose results depend only on hashable arguments and stable external state. Set a size, consider memory and sensitive data, and define invalidation when dependencies change.

## Inspect memory

`tracemalloc` compares Python allocation snapshots. Generators can lower peak collection memory but suspended frames retain references. Processes duplicate or copy memory differently by platform. Measure peak and retained memory under a real workload.

## Preserve correctness

Keep tests green, measure before and after, record the environment, and revert changes that do not improve the target. Readability is a performance feature for maintenance unless evidence justifies complexity.

## Check your understanding

You are ready when you can separate debugging, profiling, complexity, and optimization and provide measurements for a claim.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
