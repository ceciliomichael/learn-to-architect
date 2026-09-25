# Module 07: Compound Values with Tuples and Arrays

## Outcome

Group related values with tuples, work with fixed-size arrays, destructure data, and recognize safe versus unsafe indexing assumptions.

## Why this matters

Single scalar values are not enough to model most information. Programs constantly group values: coordinates, color channels, dimensions, measurements, and fixed sets of configuration values.

## Programming concept

A compound value groups multiple values into one larger value. A tuple can hold fields of different types in fixed positions. An array stores a fixed number of values of one type. Indexing chooses an element by numeric position, usually starting at zero.

## Rust model

Rust tuples use parentheses and can mix types. Arrays use square brackets and have their length in the type, such as [i32; 3]. Tuple destructuring binds individual parts by pattern. Array indexing is checked; an out-of-bounds runtime index causes a panic rather than reading arbitrary memory.

## Local Cargo example

~~~text
cargo new compound_values --edition 2024
cd compound_values
~~~

Replace src/main.rs:

~~~rust
fn main() {
    let point = (12.5, -3.0);
    let (x, y) = point;

    let readings = [18, 21, 20, 23];
    let first = readings[0];

    println!("point: ({x}, {y})");
    println!("first reading: {first}");
    println!("reading count: {}", readings.len());
}
~~~

Run cargo check, cargo run, and cargo fmt.

Expected output:

~~~text
point: (12.5, -3)
first reading: 18
reading count: 4
~~~


## Walkthrough

- The tuple stores two floating-point coordinates.
- Destructuring gives names to tuple positions.
- The array contains four integers of one element type.
- Index zero is the first element.
- len reports the fixed array length through a familiar method interface.

## Deliberate mistake

~~~rust
fn main() {
    let values = [10, 20, 30];
    let index = 9;
    println!("{}", values[index]);
}
~~~

The index is valid as a type but invalid for this array at runtime. Rust performs bounds checking and the program panics rather than reading outside the array.

Corrected version:

~~~rust
fn main() {
    let values = [10, 20, 30];
    let index = 9;

    match values.get(index) {
        Some(value) => println!("{value}"),
        None => println!("no value at index {index}"),
    }
}
~~~

## Mental model

- Use a tuple for a small fixed grouping whose positions have distinct roles.
- Use an array for a fixed-size homogeneous sequence.
- Indices start at zero.
- A valid integer index type does not guarantee the index is within bounds.
- Prefer checked access when an index comes from uncertain input.

## Common mistakes

- Using a tuple when a named struct would make fields much clearer.
- Assuming array length can grow at runtime.
- Forgetting zero-based indexing.
- Trusting an external index without checking it.
- Confusing [value; count] repetition syntax with a list of different elements.

## Transfer to other languages

Tuples, records, arrays, lists, and sequences appear across languages. The fixed-versus-dynamic distinction and the need to validate indices are universal even when syntax and bounds behavior differ.

## Guided practice

1. Create a tuple containing a name, age, and active flag, then destructure it.
2. Create an array of five scores and print the first and last.
3. Use values.get with an invalid index.
4. Create an array using repeated-value syntax.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before reading the answers.

## Readiness check

- choose between tuple and fixed array;
- destructure a tuple;
- explain zero-based indexing;
- explain why checked access matters for uncertain indices.

## Next

Continue to [Module 08](../08-ownership-moves-copy-clone-and-drop/README.md).
