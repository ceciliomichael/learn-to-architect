# Module 19: Work with JSON and CSV Data

## What you will learn

You will serialize common data, validate decoded shapes, and read CSV rows without newline mistakes.

## JSON maps a limited set of values

```python
import json

record = {"name": "Ava", "score": 92, "active": True, "note": None}
text = json.dumps(record, ensure_ascii=False, indent=2)
restored = json.loads(text)
```

JSON supports objects with string keys, arrays, strings, numbers, booleans, and null. Tuples become arrays and return as lists. Sets, Decimal, dates, and custom objects need an explicit representation.

JSON is data, not executable Python. Never use `eval` to decode it.

## Read and write JSON files

```python
from pathlib import Path

path = Path("record.json")
with path.open("w", encoding="utf-8") as file:
    json.dump(record, file, ensure_ascii=False, indent=2)

with path.open("r", encoding="utf-8") as file:
    loaded = json.load(file)
```

Decoding proves only that syntax is valid JSON. Validate the expected top-level type, required keys, value types, ranges, sizes, and allowed strings before use.

## CSV stores rows of text fields

```python
import csv

with open("people.csv", "w", encoding="utf-8", newline="") as file:
    writer = csv.DictWriter(file, fieldnames=["name", "score"])
    writer.writeheader()
    writer.writerow({"name": "Ava", "score": 92})
```

Use `newline=""` as required by Python's CSV documentation so the module manages newline conventions correctly.

```python
with open("people.csv", "r", encoding="utf-8", newline="") as file:
    for row in csv.DictReader(file):
        score = int(row["score"])
        print(row["name"], score)
```

CSV fields are read as strings unless a chosen reader option or your code converts them. Validate headers before indexing required fields.

## Spreadsheet formula injection

When untrusted CSV will be opened in a spreadsheet, cells beginning with characters such as `=`, `+`, `-`, or `@` may be interpreted as formulas. Sanitization depends on the receiving spreadsheet and business requirement. Prefer formats and import controls that keep untrusted text as text.

## Bound untrusted input

Limit file size, nesting, row counts, field lengths, and numeric ranges before allocating or processing large external data. Standard decoders are not complete schema validators.

## Check your understanding

You are ready when you can round-trip supported data and explain why parsing must be followed by schema validation.
