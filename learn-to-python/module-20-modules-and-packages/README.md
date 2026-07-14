# Module 20: Modules, Imports, and Packages

## What you will learn

You will split code into modules, control script entry, create a package, and avoid import-time surprises.

## A module is importable Python code

Create `prices.py`:

```python
def subtotal(price, quantity):
    return price * quantity
```

Use it from `app.py` in the same folder:

```python
from prices import subtotal

print(subtotal(12.5, 3))
```

An import finds a module, creates its module object, and executes its top-level code the first time in that process. Later ordinary imports reuse the cached module.

Keep top-level behavior small. Do not start servers, ask for input, or perform important writes merely because a module was imported.

## Use a main function and guard

```python
def main():
    print("Program started")

if __name__ == "__main__":
    main()
```

When the file runs as the entry script, `__name__` is `"__main__"`. When imported, it is the module name. The guard keeps entry behavior from running during import and tests.

## Import styles

```python
import math
print(math.sqrt(9))

from pathlib import Path
```

Qualified names such as `math.sqrt` show their source and reduce collisions. Avoid `from module import *`; it hides which names enter the module.

## A package groups modules

```text
shop/
  __init__.py
  prices.py
  reports.py
run_shop.py
```

In `reports.py`:

```python
from shop.prices import subtotal
```

Use absolute imports for clear application structure. Relative imports can be appropriate inside a library package but depend on package execution context.

Run package-aware code from its project root:

```text
python -m shop.reports
```

Do not run an internal package file by path and then repair import failures by changing `sys.path` inside source code.

## Avoid circular imports

If `prices` imports `reports` while `reports` imports `prices`, one module can be only partly initialized. Move shared definitions to a lower-level module, pass dependencies, or redesign responsibilities.

## Check your understanding

You are ready when you can predict import-time execution, use a main guard, and draw a package dependency direction without a cycle.
