# Module 04: Operators, Conversion, and Basic Input/Output

## Outcome

Perform arithmetic and comparisons, combine Boolean conditions, read terminal input, and parse or explicitly convert values.

## Why this matters

Real programs cross boundaries. Data often arrives as text or bytes while the program needs a number or structured value. Converting external representation into validated internal data is a core responsibility.

## Programming concept

Operators transform or compare values. Input brings data into a program; output sends data out. Parsing interprets a representation according to rules. Conversion changes from one representation or type to another.

## Rust model

Rust type-checks operators and avoids many silent numeric conversions. std::io provides standard input. read_line appends into a String. Parsing returns Result because input may be invalid. We match it directly here; Module 14 develops the complete error model.

## Work in a real Cargo project

From your practice directory:

~~~text
cargo new basic_io --edition 2024
cd basic_io
~~~

Replace src/main.rs with:

~~~rust
use std::io;

fn main() {
    println!("Enter an integer:");

    let mut input = String::new();
    io::stdin()
        .read_line(&mut input)
        .expect("failed to read standard input");

    let number: i32 = match input.trim().parse() {
        Ok(value) => value,
        Err(_) => {
            println!("That was not a valid integer.");
            return;
        }
    };

    println!("double: {}", number * 2);
    println!("positive and even: {}", number > 0 && number % 2 == 0);
}
~~~

Run:

~~~text
cargo check
cargo run
cargo fmt
~~~



## Walkthrough

- String::new creates a growable text buffer.
- read_line modifies the buffer through a mutable reference; borrowing is taught formally later.
- trim removes surrounding whitespace such as the newline from pressing Enter.
- The i32 annotation tells parse which number type to produce.
- Remainder zero after division by two indicates an even integer.

## Deliberate mistake

~~~rust
fn main() {
    let whole: i32 = 5;
    let decimal: f64 = whole;
    println!("{decimal}");
}
~~~

Rust does not silently convert this integer into a floating-point value. The representation change must be explicit.

Corrected version:

~~~rust
fn main() {
    let whole: i32 = 5;
    let decimal: f64 = whole as f64;
    println!("{decimal}");
}
~~~

Do not memorize the correction. State the rule that the original program violated.

## Mental model

- External input begins untrusted.
- Parse at the boundary and handle failure.
- Do not assume numeric types convert implicitly.
- Integer and floating-point arithmetic have different representation rules.
- Name complex conditions when Boolean expressions become hard to read.

## Common mistakes

- Forgetting to trim terminal input before parsing.
- Using expect for ordinary invalid user input.
- Expecting integer 5 / 2 to produce 2.5.
- Casting without considering range or precision.
- Writing a long Boolean expression with no meaningful intermediate names.

## Transfer to other languages

Every language has representation boundaries. Some coerce values automatically and some require explicit conversion, but parsing, validation, range, precision, and failure remain universal concerns.

## Guided practice

1. Read an integer and print its square.
2. Test a range condition with logical AND.
3. Enter non-numeric text and follow the failure branch.
4. Convert an i32 to f64 and divide by 2.0.

## Independent exercise and quiz

Complete [the exercises](exercise/exercise.md), then [the quiz](quiz/quiz.md). Attempt both before opening the answer directories.

## Readiness check

You are ready to continue when you can:

- use arithmetic, comparison, remainder, and Boolean operators;
- read a line from standard input;
- explain why parsing can fail;
- identify an explicit numeric conversion and possible range or precision consequences.

## Next

Continue to [Module 05](../05-expressions-decisions-and-loops/README.md).
