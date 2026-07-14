# Exercise solution

```rust
use std::fs::{self, File};
use std::io::{self, Read};
use std::path::Path;

fn read_preview(path: &Path, limit: u64) -> io::Result<String> {
    let file = File::open(path)?;
    let mut bounded = file.take(limit);
    let mut text = String::new();
    bounded.read_to_string(&mut text)?;
    Ok(text)
}

fn run() -> io::Result<()> {
    let path = Path::new("rust-course-preview.txt");
    fs::write(path, "one line\ntwo lines\nthree lines\n")?;

    let preview_result = read_preview(path, 40);
    let remove_result = fs::remove_file(path);
    let preview = preview_result?;
    remove_result?;

    println!("{preview}");
    Ok(())
}

fn main() {
    if let Err(error) = run() {
        eprintln!("file operation failed: {error}");
        std::process::exit(1);
    }
}
```

Cleanup is attempted even if reading fails. A production application may use a temporary-file library to provide stronger cleanup behavior.
