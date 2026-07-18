# Module 27: Composition and Inheritance

## What you will learn

You will combine objects by responsibility, use inheritance only for substitutable types, and define abstract contracts.

## Composition expresses has-a relationships

```python
class EmailSender:
    def send(self, address: str, message: str) -> None:
        print(f"Sending to {address}: {message}")

class OrderService:
    def __init__(self, sender: EmailSender) -> None:
        self._sender = sender

    def confirm(self, address: str) -> None:
        self._sender.send(address, "Order confirmed")
```

OrderService has a sender. Passing the dependency makes tests and replacement clear. Prefer composition when objects have separate responsibilities or behavior may vary independently.

## Inheritance expresses is-a substitution

```python
class Notification:
    def send(self, message: str) -> None:
        raise NotImplementedError

class ConsoleNotification(Notification):
    def send(self, message: str) -> None:
        print(message)
```

A subtype should honor the base contract wherever the base is expected. It should not require stronger inputs, promise weaker results, or break important invariants.

## Abstract base classes declare runtime inheritance contracts

```python
from abc import ABC, abstractmethod

class Storage(ABC):
    @abstractmethod
    def save(self, text: str) -> None:
        pass
```

Concrete subclasses must implement abstract methods before instantiation. Protocols from Module 25 provide structural static contracts without requiring inheritance. Choose from runtime and design needs.

## Override and use super cooperatively

```python
class Named:
    def __init__(self, name: str) -> None:
        self.name = name

class Employee(Named):
    def __init__(self, name: str, employee_id: int) -> None:
        super().__init__(name)
        self.employee_id = employee_id
```

`super` follows the method resolution order, not merely a hardcoded parent. This matters for cooperative multiple inheritance.

Multiple inheritance can be valid for small cooperative mixins but increases method-order and initialization complexity. Avoid it for combining unrelated stateful classes.

## Do not inherit for code reuse alone

If a relationship is not truly substitutable, extract a helper or compose an object. Inheritance couples subclasses to base behavior and can create fragile hierarchies.

## Check your understanding

You are ready when you can say has-a or is-a, test substitutability, and choose ABC, protocol, or composition from the contract.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
