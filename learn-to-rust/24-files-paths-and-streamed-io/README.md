# Module 24: Files, Paths, and Streamed I/O

Use `Path` for a borrowed path and `PathBuf` for an owned, changeable path. Paths are not guaranteed to be UTF-8, so do not force them into `String` unless the application requires and validates text paths.

`File::open` and `File::create` return `Result`. Wrap files with `BufReader` or `BufWriter` when processing many small pieces. Streaming avoids loading an entire untrusted file into memory.

```rust
use std::fs::File;
use std::io::{self, BufRead, BufReader};
use std::path::Path;

fn count_lines(path: &Path) -> io::Result<usize> {
    let file = File::open(path)?;
    let reader = BufReader::new(file);
    let mut count = 0;
    for line in reader.lines() {
        line?;
        count += 1;
    }
    Ok(count)
}
```

Text reading validates UTF-8. Use byte-oriented `Read` methods for arbitrary binary data. Set explicit size limits for input controlled by someone else. Check permissions and never build a trusted path by blindly joining untrusted text. Canonicalization can help inspection, but access control still needs a clear allowed directory policy and protection from filesystem races.

For important writes, write to a temporary file in the same directory, flush and synchronize as required, then replace the target using a strategy tested on each supported platform. Simple rename behavior and durability differ across operating systems and filesystems.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Continue to [Module 25](../25-serde-and-untrusted-data/README.md).
