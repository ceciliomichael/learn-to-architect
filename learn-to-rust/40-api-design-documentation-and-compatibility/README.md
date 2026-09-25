# Module 40: API Design, Documentation, and Compatibility

## Outcome

By the end of this module, you can design a small public Rust API, document caller contracts with rustdoc, use executable documentation examples, make invalid states harder to represent, and reason about compatibility before changing public behavior.

## Why this matters

Inside one private function, you can usually refactor freely as long as behavior remains correct.

A public API is different.

Once another crate, binary, teammate, or external user depends on your public function, struct, enum, trait, feature, error type, textual format, or side effect, that behavior may become part of a contract.

The larger the public surface, the more decisions you have promised to preserve.

## Programming concept

An **interface** is a contract between independently changing pieces of software.

**Encapsulation** hides representation behind behavior.

**Compatibility** means a newer version continues satisfying expectations that were part of the supported contract.

**Semantic versioning** communicates compatibility intent through version numbers, but it does not decide whether a change is actually safe.

## Rust model

Rust public API begins with pub, but good API design is not simply adding pub until another crate compiles.

Rust gives you tools for stronger interfaces:

- private fields;
- constructors;
- newtype wrappers;
- enums;
- traits;
- Result and Option;
- non-exhaustive public types when extension is deliberate;
- rustdoc;
- doctests.

The goal is to expose the smallest useful contract.

## Start with a domain type

Create:

~~~text
cargo new account_api --lib --edition 2024
cd account_api
~~~

Put this in src/lib.rs:

~~~rust
/// A validated account identifier.
///
/// Account identifiers are non-empty and contain no whitespace.
#[derive(Debug, Clone, PartialEq, Eq, Hash)]
pub struct AccountId(String);

impl AccountId {
    /// Parses a validated account identifier.
    ///
    /// # Errors
    ///
    /// Returns an error when input is empty or contains whitespace.
    ///
    /// # Examples
    ///
    /// ~~~
    /// use account_api::AccountId;
    ///
    /// let id = AccountId::parse("user-42")?;
    /// assert_eq!(id.as_str(), "user-42");
    ///
    /// # Ok::<(), String>(())
    /// ~~~
    pub fn parse(input: &str) -> Result<Self, String> {
        if input.is_empty() {
            return Err(String::from("account id cannot be empty"));
        }

        if input.chars().any(char::is_whitespace) {
            return Err(String::from("account id cannot contain whitespace"));
        }

        Ok(Self(input.to_owned()))
    }

    /// Returns the validated identifier as text.
    pub fn as_str(&self) -> &str {
        &self.0
    }
}
~~~

Run:

~~~text
cargo test
cargo test --doc
cargo doc --no-deps
~~~

## What the type guarantees

This type is stronger than exposing String directly.

Callers outside the defining module cannot construct the private inner field directly.

The public construction path validates input before creating AccountId.

That means a function taking AccountId can rely on the type's documented invariant.

This reduces repeated validation and makes illegal values harder to represent.

## Why a newtype matters

A newtype is a tuple struct containing another representation:

~~~rust
pub struct AccountId(String);
~~~

It creates a distinct type.

This prevents accidental interchange between conceptually different values that happen to share a primitive representation.

For example:

~~~rust
pub struct AccountId(String);
pub struct EmailAddress(String);
pub struct OrderId(String);
~~~

All three contain String, but they mean different things.

The compiler can now help prevent passing an email where an order ID is expected.

## Keep fields private when invariants matter

This public type is weak:

~~~rust
pub struct Account {
    pub id: String,
    pub balance_cents: i64,
    pub closed: bool,
}
~~~

Callers can create state your domain never intended.

A stronger design is:

~~~rust
pub struct Account {
    id: AccountId,
    balance_cents: u64,
    closed: bool,
}

impl Account {
    pub fn id(&self) -> &AccountId {
        &self.id
    }

    pub fn balance_cents(&self) -> u64 {
        self.balance_cents
    }

    pub fn is_closed(&self) -> bool {
        self.closed
    }
}
~~~

Construction and mutation can then flow through methods that preserve the rules.

## Public does not mean mutable

An accessor can return a shared reference without exposing mutable access to the field.

Avoid returning mutable references to invariant-bearing internals unless external mutation is truly part of the contract.

## Documentation is part of the API

Useful rustdoc should tell callers what they need to use the API correctly.

Common sections include:

- Examples
- Errors
- Panics
- Safety

Document:

- units;
- ranges;
- ownership effects;
- blocking behavior;
- allocation when materially important;
- ordering guarantees;
- failure categories;
- panic preconditions;
- thread-safety expectations;
- side effects.

Do not fill documentation with private implementation trivia that callers do not need.

## Documentation examples are tests

A rustdoc fenced code example can be compiled and run during testing.

Run:

~~~text
cargo test --doc
~~~

This reduces the chance that documentation drifts away from the real API.

## Errors are API design

A reusable public library may benefit from structured error categories when callers need different recovery behavior.

For example, a caller may want to distinguish:

- unsupported format;
- invalid data;
- permission failure;
- missing file.

The correct error design depends on what callers need to decide.

Do not create twenty error variants if every caller will report the same failure.

Do not collapse meaningful recovery categories into one vague string if callers genuinely need them.

## Panics are part of a contract too

A direct indexing API may panic on an invalid index.

If that is intentional and public, document the panic condition.

If invalid index is a normal caller possibility, a safer API may return Option instead.

Do not use panic to avoid designing an ordinary failure path.

## Public enums and compatibility

Suppose a library exposes:

~~~rust
pub enum State {
    Ready,
    Running,
}
~~~

Downstream users may write exhaustive matches.

Adding a new variant can therefore be source-breaking.

Sometimes exhaustive matching is desirable because every variant is part of the stable contract.

Sometimes you expect future variants.

Rust provides non-exhaustive annotations for APIs that deliberately reserve extension room, but use them because the contract needs extensibility, not automatically on every public enum.

## Semantic versioning

A typical version has:

~~~text
MAJOR.MINOR.PATCH
~~~

Conceptually:

- PATCH: compatible fixes;
- MINOR: compatible added functionality;
- MAJOR: incompatible API changes.

Reality requires judgment.

A change can compile and still break users through:

- changed error semantics;
- changed ordering;
- changed output format;
- changed performance characteristics;
- new panics;
- removed side effects callers depended on;
- changed feature defaults;
- changed minimum supported Rust version when that is part of the contract.

Semantic versioning is communication, not magic.

## Deliberate mistake

This API leaks representation and invalid states:

~~~rust
pub struct Percentage {
    pub value: u8,
}
~~~

A caller can construct a value over 100 even if the concept is intended to mean 0 through 100.

A better type is:

~~~rust
#[derive(Debug, Clone, Copy, PartialEq, Eq)]
pub struct Percentage(u8);

impl Percentage {
    pub fn new(value: u8) -> Result<Self, String> {
        if value > 100 {
            return Err(String::from("percentage must be 0..=100"));
        }

        Ok(Self(value))
    }

    pub fn get(self) -> u8 {
        self.0
    }
}
~~~

Now ordinary callers cannot construct an out-of-range value through the public API.

## Public representation can escape through formatting

Even when fields are private, textual representation can become a practical contract.

If users persist Display output, parse logs, script CLI output, or compare developer output in tests, changing formatting may break them.

Decide which output is intentionally stable.

Debug is primarily developer-facing and should not normally be treated as a stable serialization format.

## Keep abstractions proportional

Do not create a trait for every struct, a generic type for every value, or five wrapper layers for a private application.

A good API makes correct use easy and invalid use difficult.

It does not maximize abstraction.

## Mental model

- Public means supported contract, not merely accessible.
- Keep representation private when callers do not need it.
- Use domain types to encode meaning.
- Validate at construction when the invariant should always hold afterward.
- Document caller obligations and failure behavior.
- Test documentation examples.
- Consider compatibility before changing public behavior.
- Add abstraction only where it improves the contract.

## Common mistakes

### Everything is public

This increases the compatibility surface and lets callers depend on implementation details.

### Public mutable fields

This often destroys invariants.

### Documentation that says only what the function name says

Useful documentation explains meaning, invariants, units, failure behavior, or non-obvious contracts.

### Treating Debug as serialization

Debug is not your persistence protocol.

Use a deliberate stable format.

### Changing error strings as if they are always private

If another program parses them, you may have accidentally created a brittle external contract.

Prefer structured interfaces for machine-readable behavior.

### Hypothetical extensibility everywhere

Do not add trait objects, generics, or extension mechanisms without a real requirement.

## Transfer to other languages

The exact tools differ, but the ideas transfer to public classes and interfaces, package APIs, C headers, REST schemas, CLI commands, and database schemas.

Every external interface creates compatibility obligations.

## Guided practice

1. Run cargo doc for a library.
2. Add one doctest and verify cargo test runs it.
3. Turn a raw String identifier into a validated newtype.
4. Make invariant-bearing fields private.
5. Add an Errors section to one fallible API.
6. Add a Panics section only if the public API intentionally has a panic precondition.
7. Review one previous project and list public items that could become private.

## Exercise and quiz

Complete the exercises and quiz before opening their answers.

- [Exercises](exercise/exercise.md)
- [Quiz](quiz/quiz.md)

## Readiness check

You are ready to continue when you can:

- keep public surface intentionally small;
- use a newtype for a domain distinction;
- enforce an invariant through validated construction;
- write useful rustdoc;
- run doctests;
- explain API compatibility beyond compilation;
- identify when public formatting or errors become contracts.

## Next

Continue to [Module 41](../41-architecture-and-dependency-boundaries/README.md).
