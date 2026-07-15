# Module 18: Read and Write Files with pathlib

## What you will learn

You will construct paths, read and write encoded text, manage file lifetime, and replace files more safely.

## Paths are not manual strings

```python
from pathlib import Path

practice_dir = Path("python-course-practice")
notes_path = practice_dir / "notes.txt"
practice_dir.mkdir(parents=True, exist_ok=True)
```

`Path` handles platform separators and offers explicit filesystem operations. A relative path is resolved from the process working directory, not automatically from the script's folder.

Inspect deliberately:

```python
print(Path.cwd())
print(notes_path.resolve())
```

## Read and write text with encoding

```python
notes_path.write_text("First note\n", encoding="utf-8")
text = notes_path.read_text(encoding="utf-8")
```

`write_text` replaces existing content. That is convenient but dangerous when overwrite is not intended.

For streaming or appending, use `open` through a context manager:

```python
with notes_path.open("a", encoding="utf-8", newline="") as file:
    file.write("Second note\n")
```

The `with` statement closes the file even when work raises an exception.

## Text and bytes are different

Text is decoded Unicode. Bytes are raw values:

```python
data_path = practice_dir / "sample.bin"
data_path.write_bytes(b"\x00\x01")
```

Encoding converts text to bytes. Decoding converts bytes to text. Never guess an encoding for external data; use its documented format.

## Process large files incrementally

```python
with notes_path.open("r", encoding="utf-8") as file:
    for line_number, line in enumerate(file, start=1):
        print(line_number, line.rstrip("\n"))
```

Iteration avoids loading the whole file. Remove only the newline you mean to remove; plain `strip` can discard meaningful spaces.

## Replace important content more safely

Write a complete temporary file in the same directory, flush and close it, then replace the destination:

```python
temporary = notes_path.with_suffix(".tmp")
temporary.write_text("Replacement\n", encoding="utf-8")
temporary.replace(notes_path)
```

Replacement atomicity and durability depend on operating system and filesystem. Real critical data also needs validation, backups, permissions, and recovery tests.

## Treat paths as untrusted at boundaries

Do not join a user-supplied path and assume it remains inside an allowed directory. Resolve it and enforce the intended root, avoid following unsafe links where the threat model matters, and use generated server-side names for uploads.

## Check your understanding

You are ready when you can explain working-directory-relative paths, encoding, context cleanup, and overwrite risk.
