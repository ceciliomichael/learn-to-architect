# Checkpoint Project A: Command-Line Utility

## Goal

Build a local interactive unit converter using only the Rust standard library.

This checkpoint combines the first six modules: Cargo, the compile-run loop, values and types, parsing, control flow, functions, and scope.

## Required menu

~~~text
1. Celsius to Fahrenheit
2. Fahrenheit to Celsius
3. Kilometers to Miles
4. Miles to Kilometers
5. Quit
~~~

For each conversion, ask for a value, parse it as f64, compute the result, print a useful label, then return to the menu.

Invalid menu input and invalid numbers must produce a useful message and continue instead of terminating unexpectedly.

## Required calculation functions

~~~rust
fn celsius_to_fahrenheit(value: f64) -> f64
fn fahrenheit_to_celsius(value: f64) -> f64
fn kilometers_to_miles(value: f64) -> f64
fn miles_to_kilometers(value: f64) -> f64
~~~

Keep terminal I/O out of these calculation functions.

## Milestones

1. Make one conversion work with a hard-coded value.
2. Read and parse one f64.
3. Add the repeating menu.
4. Implement all four conversions.
5. Handle invalid input.
6. Run cargo fmt, cargo clippy, cargo check, and cargo run.

## Manual test cases

Test at least 0 C, 32 F, 1 km, 1 mi, a negative temperature, zero distance, non-numeric input, an unknown menu choice, and quit.

## Reflection

1. Which data entered as text?
2. Where did parsing and validation happen?
3. Which functions are pure calculations?
4. Which state changes while the menu runs?
5. Which concepts would remain in another language?

Continue to [Module 07](../../07-tuples-arrays-and-compound-values/README.md).
