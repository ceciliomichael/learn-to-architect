# Module 24: Test with unittest

## What you will learn

You will write repeatable unit tests, test boundaries and exceptions, and keep tests isolated.

## A test proves one behavior with evidence

`calculations.py`:

```python
def subtotal(price, quantity):
    if price < 0 or quantity < 0:
        raise ValueError("price and quantity must be nonnegative")
    return price * quantity
```

`test_calculations.py`:

```python
import unittest

from calculations import subtotal


class SubtotalTests(unittest.TestCase):
    def test_multiplies_price_and_quantity(self):
        result = subtotal(12.5, 3)
        self.assertEqual(result, 37.5)


if __name__ == "__main__":
    unittest.main()
```

Run discovery from the project root:

```text
python -m unittest discover -v
```

## Arrange, act, assert

A clear test prepares input, calls one behavior, and verifies observable output. Test names describe the rule, not an implementation step.

Test boundaries and errors:

```python
def test_zero_quantity_returns_zero(self):
    self.assertEqual(subtotal(12.5, 0), 0)

def test_negative_quantity_is_rejected(self):
    with self.assertRaisesRegex(ValueError, "nonnegative"):
        subtotal(12.5, -1)
```

Use `assertAlmostEqual` for appropriate approximate float behavior, with a deliberate tolerance. Prefer exact types when the domain requires exactness.

## Setup and cleanup

`setUp` runs before each test method and `tearDown` after it. Prefer temporary directories and fresh objects per test. Shared mutable state makes order-dependent tests.

```python
from tempfile import TemporaryDirectory

def setUp(self):
    self.temp_dir = TemporaryDirectory()

def tearDown(self):
    self.temp_dir.cleanup()
```

`addCleanup` can register cleanup immediately after acquiring a resource, reducing leaks if setup later fails.

## Mock only clear boundaries

Mocks can replace slow or nondeterministic external boundaries, but excessive mocking tests your setup rather than behavior. Pass dependencies into code, verify meaningful calls, and retain integration tests for real contracts.

## Tests are not proof of absence of bugs

They cover specified examples and properties. Combine tests with type checking, review, validation, monitoring, and clear design.

## Check your understanding

You are ready when you can test ordinary, boundary, and exceptional behavior without depending on test order.
