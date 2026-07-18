# Module 25: Protocols, Generics, and Typed Data

## What you will learn

You will preserve type relationships, describe behavior structurally, and give dictionary-shaped data precise static contracts.

## Type variables preserve relationships

```python
from typing import TypeVar

T = TypeVar("T")

def first(values: list[T]) -> T:
    if not values:
        raise ValueError("values must not be empty")
    return values[0]
```

For `list[str]`, the return is understood as `str`. One type variable connects input and output. It is not a wildcard that makes unsafe operations valid.

## Generic classes store a chosen type

```python
from typing import Generic

class Box(Generic[T]):
    def __init__(self, value: T) -> None:
        self.value = value

    def get(self) -> T:
        return self.value
```

The class syntax from Module 23 now carries a type relationship: `Box[int]` stores and returns integers.

## Protocols describe required behavior

```python
from typing import Protocol

class SupportsClose(Protocol):
    def close(self) -> None:
        pass

def finish(resource: SupportsClose) -> None:
    resource.close()
```

A static checker accepts compatible objects without explicit inheritance. This is structural typing. The empty protocol method declares the required signature. Compatible classes provide the behavior.

Protocols are primarily static. `@runtime_checkable` permits limited `isinstance` checks for member presence, but it does not verify full signatures or runtime types.

## TypedDict describes dictionary shape

```python
from typing import TypedDict

class UserRecord(TypedDict):
    user_id: int
    name: str
    active: bool
```

At runtime this is an ordinary dictionary. `TypedDict` does not validate decoded JSON. It helps static checking after boundary validation.

## Literal and NewType add meaning

```python
from typing import Literal, NewType

UserId = NewType("UserId", int)
Status = Literal["draft", "published"]

def publish(user_id: UserId, status: Status) -> None:
    print(user_id, status)
```

`Literal` restricts statically known choices. `NewType` creates a static distinction with almost no runtime wrapper cost; it is not runtime validation.

## Variance intuition

If a function only reads animals, a covariant read-only abstraction can safely accept a collection of dogs. A mutable list of dogs cannot be treated as a list of all animals because someone could append a cat. Prefer read-only abstract inputs when mutation is unnecessary.

## Check your understanding

You are ready when you can connect a generic input to its output and separate static shapes from runtime validation.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
