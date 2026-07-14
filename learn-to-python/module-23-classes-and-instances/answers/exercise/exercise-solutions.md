# Exercise Solutions: Classes and Instances

```python
class BankAccount:
    currency = "PHP"

    def __init__(self, owner: str, balance_cents: int = 0) -> None:
        owner = owner.strip()
        if not owner:
            raise ValueError("owner is required")
        if balance_cents < 0:
            raise ValueError("opening balance must be nonnegative")
        self.owner = owner
        self._balance_cents = balance_cents

    @classmethod
    def from_pesos(cls, owner: str, pesos: int) -> "BankAccount":
        if pesos < 0:
            raise ValueError("pesos must be nonnegative")
        return cls(owner, pesos * 100)

    def deposit(self, amount_cents: int) -> None:
        if amount_cents <= 0:
            raise ValueError("deposit must be positive")
        self._balance_cents += amount_cents

    def withdraw(self, amount_cents: int) -> None:
        if amount_cents <= 0:
            raise ValueError("withdrawal must be positive")
        if amount_cents > self._balance_cents:
            raise ValueError("insufficient balance")
        self._balance_cents -= amount_cents

    @property
    def balance_cents(self) -> int:
        return self._balance_cents

    def display_balance(self) -> str:
        return f"{self.currency} {self._balance_cents / 100:.2f}"

first = BankAccount("Ava", 1000)
second = BankAccount.from_pesos("Ben", 20)
first.deposit(250)
second.withdraw(500)
print(first.balance_cents, first.display_balance())
print(second.balance_cents, second.display_balance())
```

Each constructor creates its own balance attribute, so changing one account does not change the other.

This class demonstrates the shared mutable attribute mistake:

```python
class WrongCart:
    items: list[str] = []

wrong_first = WrongCart()
wrong_second = WrongCart()
wrong_first.items.append("shared")
print(wrong_second.items)

class Cart:
    def __init__(self) -> None:
        self.items: list[str] = []

right_first = Cart()
right_second = Cart()
right_first.items.append("independent")
print(right_second.items)
```

`wrong_second` sees the shared item. `right_second` remains empty because `Cart.__init__` creates a list for each instance.

Verify invalid cases at the public methods:

```python
invalid_actions = [
    lambda: BankAccount("   "),
    lambda: BankAccount("Ava", -1),
    lambda: BankAccount("Ava").deposit(0),
    lambda: BankAccount("Ava", 100).withdraw(101),
]

for action in invalid_actions:
    try:
        action()
    except ValueError as error:
        print(error)
```

All four actions raise a clear `ValueError` before invalid state can be stored.

Use a custom exception when stock failure needs its own category and structured details:

```python
class InsufficientStockError(Exception):
    def __init__(self, requested: int, available: int) -> None:
        self.requested = requested
        self.available = available
        super().__init__(f"requested {requested}, available {available}")

def reserve(requested: int, available: int) -> None:
    if requested > available:
        raise InsufficientStockError(requested, available)

try:
    reserve(8, 3)
except InsufficientStockError as error:
    print(error.requested, error.available, str(error))
```

The handler can catch this business failure without also catching every unrelated `ValueError`.
