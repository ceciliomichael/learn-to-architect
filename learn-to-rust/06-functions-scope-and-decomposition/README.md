# Module 06: Functions, Scope, and Decomposition

## Outcome

Define functions with typed inputs and outputs, understand local scope and a basic call-stack model, and decompose a problem into named responsibilities.

## Why this matters

A program with every operation inside main becomes difficult to read, test, and change. Functions let you name behavior and make its required inputs and produced outputs explicit.

## Programming concept

A function is a named unit of behavior with an interface. A parameter is an input name in the definition; an argument is supplied by a caller. Scope determines where a name is valid. The call stack tracks active function calls and where execution returns.

## Rust model

Rust declares functions with fn. Parameter and return types are explicit in signatures. A final expression without a semicolon can be the return value. Blocks create scopes. Local bindings are unavailable after their scope ends.

## Work in a real Cargo project

From your practice directory:

~~~text
cargo new functions_and_scope --edition 2024
cd functions_and_scope
~~~

Replace src/main.rs with:

~~~rust
fn area(width: u32, height: u32) -> u32 {
    width * height
}

fn is_large(area: u32) -> bool {
    area >= 100
}

fn main() {
    let rectangle_area = area(12, 9);
    println!("area: {rectangle_area}");
    println!("large: {}", is_large(rectangle_area));
}
~~~

Run:

~~~text
cargo check
cargo run
cargo fmt
~~~

Expected output:

~~~text
area: 108
large: true
~~~


## Walkthrough

- area has two u32 parameters and returns u32.
- width * height is a final expression, so its value is returned.
- is_large computes one Boolean decision without unrelated work.
- main coordinates the higher-level flow.
- After a function returns, execution resumes at its caller.

## Deliberate mistake

~~~rust
fn double(value: i32) -> i32 {
    value * 2;
}

fn main() {
    println!("{}", double(4));
}
~~~

The semicolon discards the final expression value. The body then produces unit, which does not match the promised i32 return type.

Corrected version:

~~~rust
fn double(value: i32) -> i32 {
    value * 2
}

fn main() {
    println!("{}", double(4));
}
~~~

Do not memorize the correction. State the rule that the original program violated.

## Mental model

- A function signature is an input/output contract.
- Prefer one coherent responsibility per function.
- Local names live only in their scopes.
- Expressions produce values; semicolons often turn expression use into statements.
- Pass results through return values instead of hidden global state.

## Common mistakes

- Adding a semicolon to a final expression that should be returned.
- Writing giant functions because decomposition feels like extra code.
- Splitting code into meaningless tiny functions.
- Hiding inputs in global state.
- Confusing parameters with arguments.

## Transfer to other languages

Functions, methods, procedures, and closures differ across languages, but decomposition, explicit inputs, outputs, local scope, and call relationships are universal.

## Guided practice

1. Write an add function taking two i32 values.
2. Write an is_even function returning bool.
3. Move a calculation out of main.
4. Create an inner block and verify a local binding cannot be used after the block.

## Independent exercise and quiz

Complete [the exercises](exercise/exercise.md), then [the quiz](quiz/quiz.md). Attempt both before opening the answer directories.

## Readiness check

You are ready to continue when you can:

- write a typed function signature;
- return a final expression;
- explain parameter versus argument;
- describe local scope and a basic call stack;
- split a small problem into clear functions.

## Next

Continue to [Checkpoint Project A](../projects/project-a-command-line-utility/README.md).
