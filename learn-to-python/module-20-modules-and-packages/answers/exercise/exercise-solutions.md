# Exercise Solutions: Modules, Imports, and Packages

`calculations.py`:

```python
def subtotal(price, quantity):
    return price * quantity

def add_tax(amount, rate):
    return amount * (1 + rate)
```

`app.py`:

```python
from calculations import add_tax, subtotal

def main():
    before_tax = subtotal(12.5, 3)
    print(add_tax(before_tax, 0.08))

if __name__ == "__main__":
    main()
```

`check_import.py`:

```python
import app

print("Import completed without starting app.main")
```

Create the package beside those files:

```text
learning_tools/
  __init__.py
  numbers.py
  text.py
```

`learning_tools/text.py`:

```python
def clean_label(text: str) -> str:
    return " ".join(text.split()).title()
```

`learning_tools/numbers.py`:

```python
def double(value: float) -> float:
    return value * 2

def main() -> None:
    print(double(6))

if __name__ == "__main__":
    main()
```

`learning_tools/__init__.py`:

```python
from learning_tools.numbers import double
from learning_tools.text import clean_label

__all__ = ["clean_label", "double"]
```

From the project root, run `python app.py`, `python check_import.py`, and `python -m learning_tools.numbers`. The first command prints the calculated total, the second prints only its confirmation line, and the third prints `12`. Running with `-m` preserves the package context.
