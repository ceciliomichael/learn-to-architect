# Exercise Solutions: Work with JSON and CSV Data

```python
import csv
import json
from pathlib import Path

books = [
    {"title": "First Steps", "price": 12.5},
    {"title": "Clear Python", "price": 18.0},
    {"title": "Reliable Data", "price": 21.75},
]
json_path = Path("books.json")
json_path.write_text(json.dumps(books, ensure_ascii=False, indent=2), encoding="utf-8")
loaded = json.loads(json_path.read_text(encoding="utf-8"))

if not isinstance(loaded, list):
    raise ValueError("top-level JSON must be a list")
for item in loaded:
    if not isinstance(item, dict):
        raise ValueError("each book must be an object")
    if not isinstance(item.get("title"), str):
        raise ValueError("title must be text")
    price = item.get("price")
    if not isinstance(price, (int, float)) or isinstance(price, bool) or price < 0:
        raise ValueError("price must be a nonnegative number")

csv_path = Path("books.csv")
with csv_path.open("w", encoding="utf-8", newline="") as file:
    writer = csv.DictWriter(file, fieldnames=["title", "price"])
    writer.writeheader()
    writer.writerows(books)

with csv_path.open("r", encoding="utf-8", newline="") as file:
    reader = csv.DictReader(file)
    if reader.fieldnames is None or not {"title", "price"} <= set(reader.fieldnames):
        raise ValueError("required CSV headers are missing")
    for row in reader:
        print(row["title"], float(row["price"]))
```
