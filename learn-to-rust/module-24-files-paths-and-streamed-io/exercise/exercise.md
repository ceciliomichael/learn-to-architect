# Exercise: Read a bounded text file

Write `read_preview(path: &Path, limit: u64) -> io::Result<String>`.

1. Open the file without changing it.
2. Use `Read::take` so no more than `limit` bytes are read.
3. Read into a string and return it.
4. In `main`, write a small practice file, read at most 40 bytes, and print the preview.
5. Remove the practice file and handle every error with `Result`.
