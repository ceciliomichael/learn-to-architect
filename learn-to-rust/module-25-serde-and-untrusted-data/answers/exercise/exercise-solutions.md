# Exercise solution

Add the dependencies:

```text
cargo add serde --features derive
cargo add serde_json
```

Use this `src/main.rs`:

```rust
use serde::Deserialize;

#[derive(Deserialize)]
#[serde(deny_unknown_fields)]
struct RawSettings {
    username: String,
    refresh_seconds: u64,
}

struct Settings {
    username: String,
    refresh_seconds: u64,
}

impl Settings {
    fn username(&self) -> &str {
        &self.username
    }

    fn refresh_seconds(&self) -> u64 {
        self.refresh_seconds
    }
}

impl TryFrom<RawSettings> for Settings {
    type Error = String;

    fn try_from(raw: RawSettings) -> Result<Self, Self::Error> {
        let username = raw.username.trim();
        if username.is_empty() {
            return Err(String::from("username must not be blank"));
        }
        if !(5..=3600).contains(&raw.refresh_seconds) {
            return Err(String::from("refresh_seconds must be from 5 through 3600"));
        }
        Ok(Self {
            username: username.to_owned(),
            refresh_seconds: raw.refresh_seconds,
        })
    }
}

fn run() -> Result<(), String> {
    let json = r#"{"username":"Mira","refresh_seconds":30}"#;
    let raw: RawSettings =
        serde_json::from_str(json).map_err(|error| format!("invalid JSON: {error}"))?;
    let settings = Settings::try_from(raw)?;
    println!(
        "{}: {} seconds",
        settings.username(),
        settings.refresh_seconds()
    );
    Ok(())
}

fn main() {
    if let Err(error) = run() {
        eprintln!("settings error: {error}");
        std::process::exit(1);
    }
}
```

Parsing and domain validation are separate. The rest of the program receives only a valid `Settings` value.
