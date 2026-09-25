# Exercise Solutions: Module 42

## 1. Trace the scaling

The pairwise algorithm has quadratic comparison growth in the worst case.

The hash-set algorithm uses additional auxiliary memory for the set.

You cannot declare one implementation universally better from Big O alone.

For tiny bounded input, the simple pairwise scan may be perfectly adequate and can avoid hashing/allocation.

For large input, the scaling difference often dominates.

Measure the workload that matters.

## 2. Repair the benchmark process

A good experiment isolates cause and effect.

Example:

~~~text
Workload:
process 100,000 representative records

Build:
cargo build --release

Correctness:
same automated tests for old and new implementations

Baseline:
20 repeated runs after a documented warm-up policy

Change:
replace only the duplicate-detection algorithm

New measurement:
same machine, input, build profile, and run procedure

Result:
compare distributions and record uncertainty
~~~

The exact number of repetitions depends on the workload. The important part is repeatability and comparable behavior.

## 3. Modify an allocation pattern

with_capacity attempts to allocate enough vector storage up front so growth does not repeatedly allocate larger buffers.

It does not mean zero allocation. The vector normally still allocates its backing storage.

Measurement remains necessary because growth may not have been a meaningful bottleneck.

## 4. Build a performance investigation

There is no single code solution.

A strong report distinguishes:

- measured evidence;
- hypothesis;
- change;
- result.

Do not rewrite several unrelated parts and then attribute the result to one guessed cause.

Reverting an optimization that does not justify its complexity is a successful engineering outcome.
