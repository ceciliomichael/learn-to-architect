# Module 36: Measure and Improve Performance

Performance work begins with a user-visible goal and evidence. Measure a representative workload in a release build:

```text
cargo build --release
cargo run --release
```

Debug builds favor fast compilation and safety checks, so their timing does not represent optimized production code. Run enough samples to see normal variation, keep input and machine conditions comparable, and measure the whole behavior users care about.

A profiler shows where time is actually spent. Platform tools can sample CPU use, allocations, I/O waits, and lock contention. Optimize the measured bottleneck, then measure again to verify the result and watch for regressions elsewhere.

Common useful improvements include choosing a better algorithm, avoiding unnecessary allocations or clones, reserving collection capacity when the size is known, buffering I/O, and reducing contention. Iterator code is normally optimized well, but only measurement can answer a specific case.

Do not trade correctness or a clear API for a tiny result that users cannot notice. Record the benchmark input, compiler version, target, release profile, and measurement method. Test performance changes for output equivalence.

Binary size, memory use, startup time, latency, and throughput are different goals. State which one matters and set an acceptable limit before tuning.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Continue to [Module 37](../37-dependency-and-supply-chain-security/README.md).
