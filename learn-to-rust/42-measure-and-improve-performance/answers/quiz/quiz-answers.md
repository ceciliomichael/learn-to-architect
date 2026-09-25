# Quiz Answers: Module 42

## 1

Release builds enable optimization and better represent normal production execution than development-oriented debug builds.

## 2

A benchmark measures performance of a workload. A profiler helps identify where execution time or other resources are being spent.

## 3

It describes how resource use grows as input size grows, abstracting away many constant factors.

## 4

No. Constant factors and small input sizes can make a theoretically worse-scaling algorithm faster for a bounded workload.

## 5

No. Clone cost depends on the type, size, frequency, ownership need, and whether it lies on a meaningful hot path.

## 6

Rust's optimizer can often inline and optimize iterator abstractions aggressively. Source style alone does not determine machine-code performance.

## 7

Operating-system scheduling, cache state, CPU frequency, initialization, thermal behavior, and other noise can distort one measurement.

## 8

You may make the program faster while changing required behavior, errors, security checks, or numerical semantics.

## 9

Scheduling, task creation, synchronization, queueing, context switching, and contention have real costs.

## 10

Re-run the same measurement, verify correctness, compare the benefit with complexity and resource tradeoffs, then decide whether to keep the change.
