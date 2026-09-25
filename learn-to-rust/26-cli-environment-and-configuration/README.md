# Module 26: Command-Line Interfaces, Environment, and Configuration

## Outcome

Understand process arguments and environment variables, design configuration precedence, use exit codes and stdout/stderr correctly, then adopt Clap for a production-quality CLI.

## Why this matters

Command-line programs are interfaces used by both humans and automation. A stable CLI needs predictable arguments, validation, help text, output streams, exit behavior, and configuration rules.

## Programming concept

A process interface includes arguments, environment, standard input/output/error, and exit status. Configuration often comes from several sources, so precedence must be explicit. Secrets require different handling from ordinary preferences.

## Rust model

std::env::args exposes raw process arguments and std::env::var reads environment variables. For nontrivial CLIs, a maintained parser avoids reimplementing help, validation, subcommands, and edge cases. Clap is a widely used ecosystem crate; derive mode maps a typed Rust structure to CLI parsing.

## Local Cargo example

First inspect std::env::args in a disposable project. Then create cargo new task_cli --edition 2024 and run cargo add clap --features derive,env.

~~~rust
use clap::{Parser, Subcommand};

#[derive(Parser, Debug)]
#[command(version, about = "Small task CLI")]
struct Cli {
    #[arg(long, env = "TASK_FILE")]
    file: Option<String>,

    #[command(subcommand)]
    command: Command,
}

#[derive(Subcommand, Debug)]
enum Command {
    Add { title: String },
    List,
}

fn main() {
    let cli = Cli::parse();

    match cli.command {
        Command::Add { title } => println!("add: {title}"),
        Command::List => println!("list from {:?}", cli.file),
    }
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- The CLI shape is represented as typed structs/enums rather than manual string-position logic.
- Parser derives argument parsing and generated help.
- Subcommand maps mutually exclusive operations into an enum.
- An environment-backed value can supply configuration when the argument is absent.
- The application still owns precedence decisions and business validation beyond syntax parsing.

## Deliberate mistake

~~~rust
fn main() {
    let args: Vec<String> = std::env::args().collect();
    let file = &args[1];
    println!("opening {file}");
}
~~~

Direct positional indexing assumes an argument exists and panics when it does not. A real CLI must validate its interface and provide useful help or errors.

Corrected direction:

~~~rust
fn main() {
    let mut args = std::env::args().skip(1);
    match args.next() {
        Some(file) => println!("opening {file}"),
        None => eprintln!("usage: program FILE"),
    }
}
~~~

## Mental model

- A CLI is a public interface, not just string parsing.
- Use stdout for requested machine/user output and stderr for diagnostics.
- Exit status communicates success or failure to automation.
- Define configuration precedence explicitly, for example CLI flag over environment over config file over default.
- Do not put secrets in command-line arguments when process listings or shell history can expose them.

## Common mistakes

- Indexing raw args without validation.
- Mixing diagnostics into stdout that scripts expect to parse.
- Changing flag meanings casually after users automate them.
- Reading the same setting from several sources with undocumented precedence.
- Printing secret configuration during debugging.

## Transfer to other languages

Every operating system process has some interface to arguments, environment, I/O streams, and status. CLI parser libraries differ, but interface stability and automation-friendly behavior are universal.

## Guided practice

1. Print raw std::env::args so you see what the process receives.
2. Build a two-subcommand Clap CLI.
3. Send an error to stderr with eprintln.
4. Document one configuration key's precedence across CLI, environment, and default.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- explain process arguments, environment, stdout, stderr, and exit status;
- parse a typed CLI with Clap;
- define configuration precedence;
- identify why secrets need special handling.

## Next

Continue to [Module 27](../27-logging-diagnostics-and-debugging/README.md).
