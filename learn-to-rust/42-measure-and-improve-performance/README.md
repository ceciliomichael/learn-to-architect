# Module 42: Measure and Improve Performance

## Outcome

By the end of this module, you can define a useful performance question, measure release builds, reason about algorithmic complexity and allocation, use profiling evidence to find bottlenecks, and make optimization changes without sacrificing correctness or maintainability blindly.

## Why this matters

Performance work is unusually vulnerable to confident guessing.

A developer may assume:

- loops are faster than iterators;
- cloning is always expensive;
- heap allocation is always the bottleneck;
- unsafe code must be faster;
- more threads must improve throughput;
- a microbenchmark represents production behavior.

Any of those assumptions can be wrong for a particular workload.

Optimization begins with a question and a measurement.

## Programming concept

**Latency** measures how long one operation takes.

**Throughput** measures how much work is completed per unit of time.

**Memory usage** measures storage consumed by the process or operation.

**Algorithmic complexity** describes how resource use scales as input grows.

**Benchmarking** compares performance under controlled workloads.

**Profiling** identifies where time or resources are actually spent.

A benchmark tells you **how much**.

A profile helps tell you **where**.

## Rust model

Rust debug builds prioritize development speed and diagnostics.

Release builds enable optimization.

Compare:

~~~text
cargo run
cargo run --release
~~~

For production performance questions, debug timing is usually not representative.

Rust's ownership model can make allocations, copies, and clones visible in source, but visible does not mean important.

A correct clone that happens once during startup may matter less than a quadratic loop executed millions of times.

## Build a coarse timing experiment

Create:

~~~text
cargo new perf_basics --edition 2024
cd perf_basics
~~~

Use:

~~~rust
use std::time::Instant;

fn sum_squares(values: &[u64]) -> u64 {
    values
        .iter()
        .map(|value| value.wrapping_mul(*value))
        .fold(0_u64, u64::wrapping_add)
}

fn main() {
    let values: Vec<u64> = (0..5_000_000).collect();

    let start = Instant::now();
    let result = sum_squares(&values);
    let elapsed = start.elapsed();

    println!("result: {result}");
    println!("elapsed: {elapsed:?}");
}
~~~

Run:

~~~text
cargo run
cargo run --release
~~~

The exact timing will vary.

Do not compare your number to another person's machine as if it were a universal result.

## Why wrapping arithmetic is used here

The example intentionally performs many square-and-sum operations.

For large values, ordinary integer arithmetic may overflow depending on build settings and compiler checks.

Using explicit wrapping operations makes the arithmetic behavior part of the example instead of accidentally making overflow behavior the benchmark subject.

Performance experiments still need correct, defined behavior.

## This is not yet a rigorous benchmark

One Instant measurement includes noise from:

- process startup;
- operating-system scheduling;
- CPU frequency changes;
- background work;
- cache state;
- thermal state;
- allocator state;
- one-time initialization.

For a serious microbenchmark, use a maintained benchmark harness after reviewing it as a dependency.

The important lesson is not a specific crate.

It is the methodology:

1. define the workload;
2. warm or structure it appropriately;
3. repeat measurements;
4. analyze variation;
5. prevent the optimizer from removing the work;
6. compare equivalent behavior;
7. use realistic inputs.

## Correctness comes first

Suppose you optimize:

~~~rust
fn normalize(input: &str) -> String
~~~

Before changing its implementation, capture expected behavior in tests.

Performance improvements are regressions if they change:

- output;
- error behavior;
- ordering;
- security checks;
- numerical semantics;
- resource limits.

Keep correctness tests around the optimized path.

## Algorithmic complexity

Consider duplicate detection.

A simple nested scan:

~~~rust
fn contains_duplicate(values: &[u64]) -> bool {
    for (index, left) in values.iter().enumerate() {
        for right in &values[index + 1..] {
            if left == right {
                return true;
            }
        }
    }

    false
}
~~~

In the worst case, this compares many pairs.

Its growth is quadratic: O(n^2).

A set-based approach:

~~~rust
use std::collections::HashSet;

fn contains_duplicate(values: &[u64]) -> bool {
    let mut seen = HashSet::with_capacity(values.len());

    for value in values {
        if !seen.insert(*value) {
            return true;
        }
    }

    false
}
~~~

uses additional memory and hashing but has much better expected scaling for large inputs.

The correct choice depends on:

- input size;
- input distribution;
- memory budget;
- hash cost;
- required ordering;
- actual measurements.

Algorithmic improvement often matters more than syntax-level tuning.

## Big O is not a stopwatch

O(n) does not tell you an exact runtime.

An O(n) algorithm can be slower for tiny inputs because of larger constant costs.

An O(n^2) algorithm may be perfectly adequate when n is always below ten.

Complexity predicts scaling shape.

Measurements tell you where the practical crossover matters.

## Allocation awareness

Allocations can matter in hot paths.

Example:

~~~rust
fn labels(values: &[u64]) -> Vec<String> {
    values
        .iter()
        .map(|value| value.to_string())
        .collect()
}
~~~

This intentionally allocates owned Strings because that is the output contract.

Removing allocations may require changing the API or representation.

Do not optimize away required ownership merely to claim zero allocations.

## Preallocation

If you know the final count approximately or exactly:

~~~rust
let mut output = Vec::with_capacity(values.len());
~~~

can reduce vector growth reallocations.

But benchmark it when performance matters.

Do not add capacity calculations everywhere without evidence or a clear cheap sizing rule.

## Clone is not automatically bad

This is a poor rule:

~~~text
Never clone.
~~~

Better questions are:

- What is being cloned?
- How often?
- How large is it?
- Is independent ownership actually required?
- Is the clone on a measured hot path?
- Would avoiding it make ownership much more complex?

A clone of an Arc is very different from cloning a multi-megabyte Vec.

Even a large clone can be the right tradeoff if it simplifies infrequent work.

## Iterator versus loop

Rust iterators are designed to optimize well.

Do not assume:

~~~text
for loop = fast
iterator = slow
~~~

or the reverse.

Choose the clearest implementation first.

Then measure the actual workload.

## CPU versus I/O

If a program is mostly waiting on:

- network;
- disk;
- database;
- user input;

micro-optimizing arithmetic may not change end-to-end latency meaningfully.

A profile or system-level measurement can reveal that the process is mostly waiting rather than computing.

Performance optimization begins by locating the bottleneck class.

## Concurrency is not free performance

Adding threads or async tasks introduces costs:

- scheduling;
- synchronization;
- queueing;
- context switching;
- memory;
- contention;
- cache effects;
- coordination.

Parallelism can accelerate independent CPU work when enough cores and work exist.

Concurrency can improve utilization while waiting.

Neither is a universal speed switch.

## Profiling

A profiler can answer questions such as:

- Which functions consume CPU time?
- Where are allocations concentrated?
- Which threads are waiting?
- Where is lock contention?
- Are syscalls or network waits dominating?

Profiler tooling is operating-system specific.

Use a profiler available on your development and target platform.

Do not choose a code rewrite before looking at evidence when the performance problem is significant.

## Benchmark realistic inputs

Bad benchmark:

~~~text
sort three integers one million times
~~~

when production sorts ten million records.

Better benchmark inputs resemble:

- real size distributions;
- real data shapes;
- realistic error rates;
- realistic concurrency;
- realistic environment.

Synthetic benchmarks are still useful when they isolate one question deliberately.

Just state what they do and do not represent.

## Measure distributions, not only averages

For latency-sensitive applications, an average can hide slow outliers.

Operational systems often care about percentiles such as:

~~~text
p50
p95
p99
~~~

You do not need to become a statistics expert before measuring.

You do need to avoid presenting one average as the whole story when tail latency matters.

## Deliberate mistake

Imagine this optimization plan:

~~~text
1. Replace safe slice code with unsafe pointer arithmetic.
2. Add four worker threads.
3. Remove all clones.
4. Benchmark afterward.
~~~

This reverses the engineering process.

A better process is:

~~~text
1. Define the performance goal.
2. Capture correctness.
3. Establish a baseline.
4. Profile.
5. Identify the bottleneck.
6. Make one targeted change.
7. Re-measure.
8. Evaluate complexity and maintenance cost.
~~~

If the improvement is negligible, revert the complexity.

## Performance budgets

A useful project can define a budget such as:

~~~text
95 percent of local requests complete under 100 ms
memory remains below 200 MB for a 1 million item import
startup remains under 500 ms on target hardware
~~~

A budget makes performance a requirement that can be tested.

Avoid invented targets with no user or system need.

## Release profile awareness

Cargo supports build profiles.

Do not copy aggressive settings blindly.

Choices such as:

- optimization level;
- link-time optimization;
- code generation units;
- debug information;
- panic strategy;

can affect:

- build time;
- binary size;
- runtime performance;
- debugging;
- backtraces;
- failure semantics.

Change them only when the deployment goal justifies the trade.

## Mental model

- Performance is a requirement about a workload.
- Measure before optimizing.
- Measure release builds for production-runtime questions.
- Protect correctness before and after changes.
- Fix algorithmic scaling before tiny syntax details.
- Profile to locate the bottleneck.
- Allocation and clone cost are workload-specific.
- Concurrency adds overhead and coordination.
- Re-measure every optimization.
- Keep complexity only when the benefit justifies it.

## Common mistakes

### Optimizing debug builds

Debug performance can be dramatically different from optimized builds.

### One timing run

One number is noisy.

### Benchmarking different behavior

Two implementations must solve the same problem before comparing speed.

### Unsafe for speed before evidence

Unsafe adds proof obligations and maintenance cost.

Only consider it when safe alternatives cannot meet a measured requirement and the safety boundary can be justified.

### Microbenchmark obsession

A function can become twice as fast while end-to-end application latency changes by almost nothing.

### Ignoring memory

Faster code that uses ten times the memory may violate the real system constraint.

## Transfer to other languages

The methodology transfers completely:

- establish a baseline;
- profile;
- understand complexity;
- measure realistic workloads;
- protect correctness;
- compare tradeoffs.

Compiler and runtime behavior differ, but evidence-based optimization is universal.

## Guided practice

1. Compare one example under debug and release builds.
2. Write correctness tests for two duplicate-detection implementations.
3. Measure several input sizes.
4. Identify the scaling difference.
5. Preallocate a vector when size is known.
6. Measure whether it matters.
7. Review one clone and describe its actual cost category.
8. Identify whether your checkpoint network project is CPU-bound or I/O-bound.

## Exercise and quiz

Complete the exercises and quiz before opening the answers.

- [Exercises](exercise/exercise.md)
- [Quiz](quiz/quiz.md)

## Readiness check

You are ready to continue when you can:

- define a concrete performance question;
- explain debug versus release relevance;
- preserve correctness during optimization;
- compare algorithmic scaling;
- identify an allocation;
- explain why fewer allocations are not automatically better;
- profile before a major rewrite;
- evaluate optimization tradeoffs instead of only speed.

## Next

Continue to [Module 43](../43-dependency-and-supply-chain-security/README.md).
