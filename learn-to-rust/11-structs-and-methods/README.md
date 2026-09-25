# Module 11: Structs and Methods

## Outcome

Model domain data with named fields, attach behavior with impl blocks, and use methods that borrow, mutate, or consume self deliberately.

## Why this matters

Tuples are useful for small positional groupings, but real domain objects need names and invariants. A field named email communicates more than tuple position 2.

## Programming concept

A record groups named pieces of data. Encapsulation keeps operations near the data and can protect invariants by controlling how values are created or changed.

## Rust model

A struct defines named fields. impl blocks define associated functions and methods. A method can take &self for shared access, &mut self for mutation, or self to consume the value. Associated functions such as new are called on the type rather than an instance.

## Local Cargo example

~~~text
cargo new structs_methods --edition 2024
cd structs_methods
~~~

Replace src/main.rs:

~~~rust
struct Account {
    username: String,
    login_count: u32,
    active: bool,
}

impl Account {
    fn new(username: String) -> Self {
        Self {
            username,
            login_count: 0,
            active: true,
        }
    }

    fn record_login(&mut self) {
        self.login_count += 1;
    }

    fn summary(&self) -> String {
        format!("{}: {} logins, active={}", self.username, self.login_count, self.active)
    }
}

fn main() {
    let mut account = Account::new(String::from("ada"));
    account.record_login();
    println!("{}", account.summary());
}
~~~

Run cargo check, cargo run, and cargo fmt.

Expected output:

~~~text
ada: 1 logins, active=true
~~~


## Walkthrough

- Account gives names to related domain fields.
- new is an associated function returning Self.
- record_login uses &mut self because it changes one field.
- summary uses &self because it only reads.
- format creates and returns an owned String rather than printing directly, making the method easier to reuse and test.

## Deliberate mistake

~~~rust
struct Counter {
    value: u32,
}

impl Counter {
    fn increment(&self) {
        self.value += 1;
    }
}
~~~

A shared reference to self does not allow mutation of ordinary fields. The method contract says read-only access but its implementation tries to change state.

Corrected version:

~~~rust
struct Counter {
    value: u32,
}

impl Counter {
    fn increment(&mut self) {
        self.value += 1;
    }
}
~~~

## Mental model

- Use structs when field names communicate meaning.
- Choose method receiver by access needs: &self read, &mut self mutate, self consume.
- Constructors are conventions, not a special language keyword.
- Keep domain calculations separate from unnecessary I/O.
- Use private fields later to make invalid state harder to construct.

## Common mistakes

- Using tuple fields once the positions become hard to remember.
- Making every method mutable.
- Returning printed output instead of reusable data when the caller may need the result.
- Creating huge structs that combine unrelated responsibilities.
- Calling new a guaranteed constructor keyword; it is only a conventional associated-function name.

## Transfer to other languages

Records, classes, objects, data classes, and structs vary across languages, but named state, invariants, methods, and encapsulation are common modeling tools.

## Guided practice

1. Create a Rectangle struct and an area method.
2. Add a method that mutates one field.
3. Write an associated new function.
4. Write a method that consumes self and explain why the value cannot be used afterward.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before reading the answers.

## Readiness check

- define and instantiate a struct;
- choose a method receiver based on ownership and mutation;
- distinguish associated function from method;
- explain how named fields improve modeling.

## Next

Continue to [Module 12](../12-enums-match-and-patterns/README.md).
