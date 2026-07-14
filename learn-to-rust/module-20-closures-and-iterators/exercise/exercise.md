# Exercise: Build a score report

Given `vec![42, 81, 67, 95, 74]`:

1. Write `select_scores` that accepts a slice and a predicate implementing `Fn(i32) -> bool`.
2. Return a new vector containing matching scores.
3. Call it with a closure that keeps scores of at least 70.
4. Use an iterator to calculate the sum of the selected values.
5. Keep the original vector usable after the call.
