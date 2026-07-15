# Exercise solution

```rust
use std::env;

struct Config {
    name: String,
    count: u8,
}

fn parse_config(args: &[String]) -> Result<Config, String> {
    if args.len() != 3 {
        return Err(String::from("usage: program NAME COUNT"));
    }
    let name = args[1].trim();
    if name.is_empty() {
        return Err(String::from("NAME must not be blank"));
    }
    let count = args[2]
        .parse::<u8>()
        .map_err(|_| String::from("COUNT must be a whole number"))?;
    if !(1..=10).contains(&count) {
        return Err(String::from("COUNT must be from 1 through 10"));
    }
    Ok(Config {
        name: name.to_owned(),
        count,
    })
}

fn main() {
    let args: Vec<String> = env::args().collect();
    let config = match parse_config(&args) {
        Ok(config) => config,
        Err(error) => {
            eprintln!("{error}");
            std::process::exit(2);
        }
    };

    for _ in 0..config.count {
        println!("{}", config.name);
    }
}
```

Parsing is isolated from process exit behavior, so tests can call `parse_config` directly.
