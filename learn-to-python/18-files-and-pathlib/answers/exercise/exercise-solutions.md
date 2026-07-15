# Exercise Solutions: Read and Write Files with pathlib

```python
from pathlib import Path

directory = Path("file-practice")
directory.mkdir(exist_ok=True)
path = directory / "notes.txt"
path.write_text("one\ntwo\nthree\n", encoding="utf-8")
print(path.read_text(encoding="utf-8"))

with path.open("r", encoding="utf-8") as file:
    for number, line in enumerate(file, start=1):
        print(number, line.rstrip("\n"))

with path.open("a", encoding="utf-8", newline="") as file:
    file.write("four\n")

temporary = path.with_suffix(".tmp")
temporary.write_text("new one\nnew two\n", encoding="utf-8")
temporary.replace(path)

try:
    (directory / "missing.txt").read_text(encoding="utf-8")
except FileNotFoundError:
    print("The expected practice file is missing.")
```

Only the explicitly expected missing-file failure is handled.
