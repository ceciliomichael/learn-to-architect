# Exercises: Module 42

## 1. Trace the scaling

Compare:

~~~text
Algorithm A:
compare every value with every later value

Algorithm B:
insert each value into a hash set and stop on repeated insertion
~~~

For increasing n:

1. Which algorithm has worse worst-case comparison growth?
2. Which uses more auxiliary memory?
3. Can you declare a winner for every workload without measuring?

Explain.

## 2. Repair the benchmark process

A teammate says:

~~~text
I changed five things and the program feels faster.
~~~

Write a better experiment containing:

- one workload;
- release build;
- correctness check;
- baseline;
- one primary change;
- repeated measurements;
- recorded environment assumptions.

## 3. Modify an allocation pattern

Start from code that repeatedly pushes into an empty Vec when the final output count is already known.

Use with_capacity.

Then answer:

- What reallocation does this attempt to avoid?
- Does the code now have zero allocations?
- Why must you still measure before claiming an improvement?

## 4. Build a performance investigation

Choose one previous course project.

Write PERFORMANCE.md containing:

1. the user-visible or system-visible metric;
2. representative workload;
3. baseline procedure;
4. correctness tests;
5. profile or instrumentation evidence;
6. suspected bottleneck;
7. one change;
8. new measurement;
9. tradeoff;
10. final decision: keep, revert, or investigate further.

A valid result is **no optimization needed** if evidence does not justify complexity.
