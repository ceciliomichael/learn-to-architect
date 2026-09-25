# Module 25: Serialization with Serde and Untrusted Data

## Outcome

Serialize and deserialize structured JSON with Serde, distinguish syntax validity from domain validity, and treat external data as untrusted input.

## Why this matters

Applications persist state and communicate through formats such as JSON. Turning structured in-memory values into bytes or text is serialization; reversing that process is deserialization. Parsed data can still violate your business rules.

## Programming concept

A wire or storage format is an external representation. A schema describes expected shape and types. Parsing validates representation and structure, while domain validation checks meaning: ranges, relationships, permissions, size limits, and invariants.

## Rust model

Serde provides serialization/deserialization traits used by format crates such as serde_json. Derive macros generate implementations for structs and enums. serde_json::from_str returns Result, but successful deserialization only means the JSON matched the requested Rust shape. Your code must still validate domain rules and resource limits.

## Local Cargo example

Create cargo new serde_data --edition 2024, then run cargo add serde --features derive and cargo add serde_json.

~~~rust
use serde::{Deserialize, Serialize};

#[derive(Debug, Serialize, Deserialize)]
struct Settings {
    username: String,
    refresh_seconds: u64,
}

impl Settings {
    fn validate(&self) -> Result<(), String> {
        if self.username.trim().is_empty() {
            return Err(String::from("username cannot be empty"));
        }
        if !(1..=3600).contains(&self.refresh_seconds) {
            return Err(String::from("refresh_seconds must be 1..=3600"));
        }
        Ok(())
    }
}

fn main() -> Result<(), Box<dyn std::error::Error>> {
    let text = r#"{"username":"ada","refresh_seconds":30}"#;
    let settings: Settings = serde_json::from_str(text)?;
    settings.validate()?;

    let encoded = serde_json::to_string_pretty(&settings)?;
    println!("{encoded}");
    Ok(())
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- Derive creates Serde trait implementations from the struct shape.
- from_str verifies JSON syntax and that required fields can be represented as the requested Rust field types.
- validate applies domain rules that JSON syntax cannot know.
- to_string_pretty serializes trusted in-memory state back into JSON.
- Box<dyn Error> is used only as a convenient application boundary here; trait objects are explained later.

## Deliberate mistake

~~~rust
use serde::Deserialize;

#[derive(Deserialize)]
struct User {
    is_admin: bool,
}

fn main() {
    let incoming = r#"{"is_admin":true}"#;
    let user: User = serde_json::from_str(incoming).unwrap();
    if user.is_admin {
        println!("administrator accepted");
    }
}
~~~

Deserializing a field supplied by external data does not authorize the claim. Syntax and type checks are not authentication or permission checks.

Corrected direction:

~~~rust
use serde::Deserialize;

#[derive(Deserialize)]
struct Request {
    action: String,
}

fn authorize_and_handle(request: Request, authenticated_is_admin: bool) {
    if request.action == "admin-action" && !authenticated_is_admin {
        println!("denied");
        return;
    }
    println!("request accepted");
}
~~~

## Mental model

- Deserialize means structurally interpretable, not trusted.
- Validate ranges, lengths, relationships, and permissions after parsing.
- Keep authorization data sourced from trusted identity/session state, not self-asserted payload fields.
- Place reasonable size limits before parsing data from untrusted sources.
- Plan for schema changes when persisted or networked data must survive software evolution.

## Common mistakes

- Calling successfully parsed JSON safe.
- Using unwrap on malformed external input.
- Letting a payload assert its own permissions.
- Accepting unbounded data size or nesting.
- Renaming/removing persisted fields without thinking about backward compatibility.

## Transfer to other languages

Every serialization system has separate representation and semantic validation concerns. JSON, Protobuf, MessagePack, database rows, and form input can all be well-formed but malicious or nonsensical.

## Guided practice

1. Add an optional field with a defaulting strategy you can explain.
2. Reject an empty username after deserialization.
3. Serialize a valid struct and read it back.
4. Feed malformed JSON and handle the error without panic.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- add Serde dependencies deliberately;
- serialize and deserialize a simple type;
- distinguish parse validity from domain validity;
- state why authorization cannot trust a payload's self-asserted role.

## Next

Continue to [Module 26](../26-cli-environment-and-configuration/README.md).
