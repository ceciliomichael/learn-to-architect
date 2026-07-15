# Exercise: Parse a repeat count

Build a program used as `cargo run -- NAME COUNT`.

1. Define `Config { name: String, count: u8 }`.
2. Write `parse_config(&[String]) -> Result<Config, String>`.
3. Require exactly two user arguments.
4. Reject a blank name and a count outside 1 through 10.
5. Print the name `count` times. Print parsing errors to stderr and exit with code 2.
