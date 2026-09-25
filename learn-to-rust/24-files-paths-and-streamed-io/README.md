# Module 24: Files, Paths, and Streamed I/O

## Outcome

Work with portable paths, read and write files through buffered streams, handle filesystem errors, and distinguish whole-file convenience from streamed processing.

## Why this matters

Programs persist configuration, import data, generate reports, and process logs. File I/O crosses into the operating system, so paths, permissions, missing files, partial work, and large data all become real concerns.

## Programming concept

A file is an operating-system resource addressed through a path. I/O can be buffered to reduce expensive system calls. Streaming processes data incrementally instead of requiring the entire input in memory. External state can change independently of your program.

## Rust model

std::path::Path and PathBuf represent filesystem paths without pretending every platform path is UTF-8 text. File opens return Result. BufReader and BufWriter add buffering. The BufRead trait supports line-oriented reading. Drop normally closes file handles, but explicit flush or successful completion still matters when reporting durable writes.

## Local Cargo example

Create cargo new file_io --edition 2024. The example writes a practice file in the current project directory and then reads it line by line.

~~~rust
use std::fs::File;
use std::io::{self, BufRead, BufReader, BufWriter, Write};
use std::path::Path;

fn write_lines(path: &Path, lines: &[&str]) -> io::Result<()> {
    let file = File::create(path)?;
    let mut writer = BufWriter::new(file);

    for line in lines {
        writeln!(writer, "{line}")?;
    }

    writer.flush()
}

fn read_lines(path: &Path) -> io::Result<()> {
    let file = File::open(path)?;
    let reader = BufReader::new(file);

    for line in reader.lines() {
        println!("{}", line?);
    }

    Ok(())
}

fn main() -> io::Result<()> {
    let path = Path::new("practice.txt");
    write_lines(path, &["first", "second", "third"])?;
    read_lines(path)
}
~~~

Run cargo check, cargo run when applicable, cargo fmt, and cargo clippy.

## Walkthrough

- Path represents a borrowed filesystem path without converting it to a String.
- File::create and File::open can fail and therefore return Result.
- BufWriter groups small writes; writeln writes through the buffer.
- flush reports an error if buffered data cannot be pushed as requested.
- BufReader processes lines incrementally rather than first loading the whole file.

## Deliberate mistake

~~~rust
use std::fs;

fn main() {
    let content = fs::read_to_string("missing.txt").unwrap();
    println!("{content}");
}
~~~

A missing file is ordinary external failure, not a reason to panic. The caller should decide whether to report, create a default, retry, or abort cleanly.

Corrected direction:

~~~rust
use std::fs;
use std::io;

fn load(path: &str) -> io::Result<String> {
    fs::read_to_string(path)
}

fn main() {
    match load("missing.txt") {
        Ok(content) => println!("{content}"),
        Err(error) => eprintln!("could not read file: {error}"),
    }
}
~~~

## Mental model

- Filesystem operations can fail even when a path was valid a moment ago.
- Use Path and PathBuf for paths, not hand-built slash-separated strings.
- Stream when data can be large or naturally processed incrementally.
- Buffer when many small reads or writes would otherwise cause repeated system calls.
- Separate parsing/domain logic from filesystem access so each can be tested independently.

## Common mistakes

- Building paths by string concatenation.
- Using unwrap for ordinary missing-file or permission errors.
- Reading enormous files entirely into memory without need.
- Assuming a successful write call means all desired data is durably stored on physical media.
- Writing directly over important data without considering interruption or atomic replacement strategy.

## Transfer to other languages

Files, paths, streams, buffers, and operating-system errors exist in every systems-facing ecosystem. APIs differ, but incremental processing and failure-aware boundaries transfer directly.

## Guided practice

1. Join a child name to a PathBuf.
2. Read a small file with read_to_string, then rewrite it with BufReader line processing.
3. Write several lines with BufWriter.
4. Make the file read function return Result rather than print inside it.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before opening the answer directories.

## Readiness check

- use Path and PathBuf appropriately;
- explain buffered versus whole-file I/O;
- propagate filesystem errors;
- separate file access from data processing.

## Next

Continue to [Module 25](../25-serde-and-untrusted-data/README.md).
