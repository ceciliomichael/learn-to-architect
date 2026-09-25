# Module 31: Declarative Macros

## Outcome

Read and write small macro_rules macros, understand token-pattern matching and repetition, and know when a normal function or generic is the better tool.

## Why this matters

Some Rust abstractions need to generate syntax rather than only compute values. Macros can accept varying numbers of tokens, create repeated syntax, or provide domain-specific notation, but they increase the amount of code a reader must mentally expand.

## Programming concept

Metaprogramming writes programs that generate or transform program syntax. It is useful when ordinary functions cannot express the required syntactic variation. The cost is an additional expansion phase and potentially harder diagnostics.

## Rust model

macro_rules! defines declarative macros with pattern arms. Fragment specifiers such as expr, ident, and ty describe accepted syntax categories. Repetition syntax can match zero or more inputs. Macros expand before normal type checking, so generated code must still satisfy Rust's rules.

## Local Cargo example

Create cargo new declarative_macros --edition 2024 and replace src/main.rs.

~~~rust
macro_rules! strings {
    ($($value:expr),* $(,)?) => {{
        let mut result = Vec::new();
        $(
            result.push($value.to_string());
        )*
        result
    }};
}

fn main() {
    let values = strings!("rust", 2026, true);
    println!("{values:?}");
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- The outer pattern accepts zero or more comma-separated expressions and an optional trailing comma.
- Each matched expression is repeated in the generated push statement.
- The double-braced expansion acts as one expression that returns result.
- Type checking happens on the expanded Rust code, so to_string must be available for each expression type.
- This macro provides variable-arity syntax that a normal fixed-arity function cannot express in the same call form.

## Deliberate mistake

~~~rust
macro_rules! only_literal {
    ($value:literal) => {
        println!("{}", $value);
    };
}

fn main() {
    let message = "hello";
    only_literal!(message);
}
~~~

The macro pattern requires a literal token, but message is an identifier expression. The mismatch occurs during macro matching before ordinary type checking.

Corrected direction:

~~~rust
macro_rules! print_expr {
    ($value:expr) => {
        println!("{}", $value);
    };
}

fn main() {
    let message = "hello";
    print_expr!(message);
}
~~~

## Mental model

- Reach for a function or generic first when ordinary values and types are sufficient.
- Macros transform syntax, not runtime values.
- Fragment specifiers define the syntax shape a macro accepts.
- Keep expansions small and predictable.
- Generated code is still subject to ownership, type, privacy, and safety rules.

## Common mistakes

- Using a macro only to save a few characters.
- Creating domain-specific syntax that no teammate can easily search or debug.
- Matching overly broad token trees when a precise fragment works.
- Hiding expensive runtime work behind a macro that looks like syntax sugar.
- Assuming macro expansion bypasses the compiler's normal checks.

## Transfer to other languages

Preprocessors, templates, AST macros, annotations, decorators, and code generation appear in many ecosystems. The transferable question is whether syntax generation earns its complexity compared with ordinary functions and types.

## Guided practice

1. Write a macro accepting one expr and printing it.
2. Add a second macro arm for zero arguments.
3. Create a repetition over comma-separated expressions.
4. Use cargo expand if you separately install an appropriate tool, or manually reason about the expansion without making the course depend on that tool.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- explain why macros operate at syntax level;
- read expr and repetition patterns;
- write a small macro_rules macro;
- choose a function instead when syntax generation is unnecessary.

## Next

Continue to [Module 32](../32-unsafe-rust-and-safety-contracts/README.md).
