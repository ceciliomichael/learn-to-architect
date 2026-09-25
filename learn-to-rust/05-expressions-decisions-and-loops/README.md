# Module 05: Expressions, Decisions, and Loops

## Outcome

Choose which code runs, repeat work safely, and use Rust's expression-oriented control flow to compute values.

## Why this matters

Useful programs react to data and repeat tasks. Control flow defines which path executes and how repetition progresses.

## Programming concept

Branching selects a path. Iteration repeats work. A condition is a Boolean decision. A useful loop has an invariant and a reason it makes progress or intentionally remains active.

## Rust model

Rust provides if, else if, else, loop, while, for, ranges, break, continue, and match. Several control-flow forms are expressions and can produce values.

## Work in a real Cargo project

From your practice directory:

~~~text
cargo new control_flow --edition 2024
cd control_flow
~~~

Replace src/main.rs with:

~~~rust
fn main() {
    let score = 83;

    let grade = if score >= 90 {
        'A'
    } else if score >= 80 {
        'B'
    } else if score >= 70 {
        'C'
    } else {
        'D'
    };

    println!("grade: {grade}");

    for attempt in 1..=3 {
        println!("attempt {attempt}");
    }

    let mut countdown = 3;
    while countdown > 0 {
        println!("{countdown}");
        countdown -= 1;
    }
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
grade: B
attempt 1
attempt 2
attempt 3
3
2
1
~~~


## Walkthrough

- The if chain computes a char assigned to grade.
- All selectable branches must produce compatible types.
- 1..=3 includes both endpoints.
- for is a good default for a known sequence.
- The while loop changes countdown, creating progress toward termination.

## Deliberate mistake

~~~rust
fn main() {
    let enabled = true;
    let message = if enabled { "on" } else { 0 };
    println!("{message}");
}
~~~

One expression cannot sometimes produce a string and sometimes an integer. Its branches need a coherent result type.

Corrected version:

~~~rust
fn main() {
    let enabled = true;
    let message = if enabled { "on" } else { "off" };
    println!("{message}");
}
~~~

Do not memorize the correction. State the rule that the original program violated.

## Mental model

- Use branching when behavior or values depend on conditions.
- Use for for sequences, while for changing conditions, and loop when explicit break defines termination.
- Every condition-driven loop needs a progress story.
- if can compute a value.
- Prefer clear control flow over clever compression.

## Common mistakes

- Forgetting to update state in a while loop.
- Producing incompatible branch types.
- Using index loops where direct iteration is clearer.
- Overusing continue until the main path is difficult to follow.
- Hiding business rules in one giant condition.

## Transfer to other languages

Branches, loops, invariants, progress, and termination are language-independent. Whether a language treats if as an expression is a semantic difference you can map later.

## Guided practice

1. Classify a temperature with an if chain.
2. Print 1 through 5 and their squares with for.
3. Count 0 to 3 with while.
4. Use loop and break with a value.

## Independent exercise and quiz

Complete [the exercises](exercise/exercise.md), then [the quiz](quiz/quiz.md). Attempt both before opening the answer directories.

## Readiness check

You are ready to continue when you can:

- choose among for, while, and loop;
- write an if expression that produces a value;
- explain how a loop progresses;
- read inclusive and exclusive ranges.

## Next

Continue to [Module 06](../06-functions-scope-and-decomposition/README.md).
