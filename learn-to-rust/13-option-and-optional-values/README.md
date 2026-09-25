# Module 13: Optional Values with Option

## Outcome

Represent absence explicitly, match Option values safely, and use convenience methods only after understanding the Some/None model.

## Why this matters

Searching may find nothing. Configuration may be missing. A user may not have a middle name. Treating absence as an ordinary value such as zero or an empty string can confuse two different meanings.

## Programming concept

Optionality means a value may legitimately be absent. A robust model distinguishes absence from a present value that happens to be zero, empty, or false.

## Rust model

Option<T> has exactly two variants: Some(T) and None. It replaces many null-style situations with an explicit type that callers must handle. Methods such as map, unwrap_or, and and_then are concise transformations, but they make sense only after the variant model is clear.

## Local Cargo example

~~~text
cargo new option_values --edition 2024
cd option_values
~~~

Replace src/main.rs:

~~~rust
fn first_even(values: &[i32]) -> Option<i32> {
    for value in values {
        if value % 2 == 0 {
            return Some(*value);
        }
    }

    None
}

fn main() {
    let values = [3, 7, 10, 11];

    match first_even(&values) {
        Some(value) => println!("first even: {value}"),
        None => println!("no even value"),
    }
}
~~~

Run cargo check, cargo run, and cargo fmt.

Expected output:

~~~text
first even: 10
~~~


## Walkthrough

- The return type states that a matching integer may be absent.
- Some wraps a found value.
- None represents a valid search result with no match.
- The caller cannot use an i32 until it has handled which variant it received.
- The function borrows the input slice and returns a copied i32, avoiding lifetime complexity here.

## Deliberate mistake

~~~rust
fn first(values: &[i32]) -> i32 {
    values[0]
}

fn main() {
    let empty: [i32; 0] = [];
    println!("{}", first(&empty));
}
~~~

The function's type claims it always returns an integer even though an empty input has no first value. Direct indexing then panics.

Corrected version:

~~~rust
fn first(values: &[i32]) -> Option<i32> {
    values.first().copied()
}

fn main() {
    let empty: [i32; 0] = [];
    println!("{:?}", first(&empty));
}
~~~

## Mental model

- Use Option when absence is a normal possibility.
- Some means present; None means absent.
- Do not invent sentinel values when absence has separate meaning.
- Match first when learning or when branches need distinct behavior.
- Use unwrap or expect only when a missing value truly violates an established invariant, not because handling None is inconvenient.

## Common mistakes

- Using zero, empty string, or false as a fake missing marker.
- Calling unwrap on external or uncertain data.
- Returning Option when failure details are actually important; Result is next.
- Nesting Option unnecessarily instead of clarifying the domain model.
- Using combinator chains so dense that the absence path becomes hard to understand.

## Transfer to other languages

Other languages use null, nullable types, Maybe, Optional, union types, or optionals. The transferable idea is to make legitimate absence part of the function's contract and handle it deliberately.

## Guided practice

1. Return Some for a found positive number and None otherwise.
2. Use match to print different messages.
3. Use unwrap_or for a harmless default.
4. Use first().copied() on an empty and non-empty integer slice.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before reading the answers.

## Readiness check

- explain Some and None;
- choose Option when absence is normal;
- avoid sentinel values for missing data;
- state when unwrap is and is not justified.

## Next

Continue to [Module 14](../14-result-and-recoverable-errors/README.md).
