# Module 21: Lifetimes

## Outcome

Read and write lifetime annotations that describe relationships between references, understand elision, and choose ownership when borrowing becomes unnecessarily complex.

## Why this matters

A reference is valid only while its referent remains alive. Rust usually infers this. When a function may return one of multiple references or a struct stores borrowed data, the relationship sometimes needs to be explicit.

## Programming concept

Reference validity is a temporal relationship: a borrowed view cannot remain usable after the value it refers to is gone. A lifetime annotation does not keep an object alive; it describes a constraint the compiler must prove.

## Rust model

Lifetime parameters use names such as 'a. In fn longer<'a>(left: &'a str, right: &'a str) -> &'a str, the output is tied to the input reference relationship. Elision rules omit annotations in common unambiguous signatures. 'static describes a reference that can remain valid for the entire program, not a request to leak ordinary values.

## Local Cargo example

Create cargo new lifetimes --edition 2024 and replace src/main.rs.

~~~rust
fn longer<'a>(left: &'a str, right: &'a str) -> &'a str {
    if left.len() >= right.len() {
        left
    } else {
        right
    }
}

struct Label<'a> {
    text: &'a str,
}

fn main() {
    let first = String::from("short");
    let second = String::from("a little longer");
    let chosen = longer(&first, &second);
    let label = Label { text: chosen };
    println!("{}", label.text);
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- The function can return either input, so the compiler needs a relationship connecting output validity to inputs.
- The annotation does not choose an input and does not extend either String's life.
- Label stores a borrowed reference, so its type records a validity relationship.
- The caller cannot keep the returned reference usable after the relevant referent ends.
- Many simple signatures rely on lifetime elision and need no explicit notation.

## Deliberate mistake

~~~rust
fn make_text() -> &str {
    let text = String::from("temporary");
    &text
}
~~~

The local String is dropped when the function returns. No lifetime annotation can make a reference to destroyed local data valid.

Corrected direction:

~~~rust
fn make_text() -> String {
    String::from("owned result")
}
~~~

## Mental model

- Lifetimes describe relationships; they do not prolong values.
- Start every lifetime problem by finding the owner.
- Returning ownership is often simpler than forcing a borrow relationship.
- Elision covers common unambiguous cases.
- A type storing a reference depends on the referent remaining valid.

## Common mistakes

- Adding 'static to make an error disappear.
- Thinking annotations control runtime duration.
- Returning references to local owned values.
- Annotating every reference unnecessarily.
- Building deeply borrowed object graphs when owned data is simpler.

## Transfer to other languages

Every language has object and resource lifetimes. Rust statically checks many reference relationships; other languages may use tracing GC, reference counting, runtime checks, or discipline. The temporal validity problem still exists.

## Guided practice

1. Read the longer signature aloud as a relationship.
2. Create a struct that stores &str.
3. Remove explicit annotations from a single-input borrowed function and observe elision.
4. Repair a bad borrowed return by returning owned data.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- state that annotations describe rather than extend lifetimes;
- identify the owner behind a returned reference;
- explain why a local reference cannot escape;
- recognize common elision;
- prefer ownership when it simplifies an API.

## Next

Continue to [Module 22](../22-closures-and-iterators/README.md).
