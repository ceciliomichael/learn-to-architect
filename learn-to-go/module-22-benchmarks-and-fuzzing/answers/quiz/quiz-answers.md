# Quiz Answers: Benchmarks and Fuzz Tests

1. The harness adjusts how many timed operation iterations run.
2. Setup would otherwise distort the measurement of the target operation.
3. A known starting input always exercised by the fuzz target.
4. Go records it so later normal tests reproduce the failure.
5. No. Results apply to the measured code, data, machine, build, and environment.
