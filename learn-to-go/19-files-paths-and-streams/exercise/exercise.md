# Exercises: Files, Paths, and Streams

1. Create a disposable directory and write a UTF-8 notes file with restrictive permissions where supported.
2. Read it line by line and number the lines.
3. Copy it with `io.Copy` instead of loading all content at once.
4. Handle one expected missing-file error with `errors.Is`.
5. Replace the file through a temporary sibling and verify final content.
