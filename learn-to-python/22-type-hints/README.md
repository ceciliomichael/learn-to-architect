# Module 22: Add Type Hints

## What you will learn

You will describe expected types for static tools while keeping runtime validation at real boundaries.

## Hints document a contract

```python
def subtotal(price: float, quantity: int) -> float:
    return price * quantity
```

Python stores annotations but normally does not enforce them when the function runs. A caller can still pass wrong objects and fail later or even receive a surprising result. Use a static type checker in development and validate untrusted runtime data explicitly.

## Annotate collections and optional values

```python
def average(values: list[float]) -> float:
    return sum(values) / len(values)

def find_name(user_id: int) -> str | None:
    if user_id == 1:
        return "Ava"
    return None
```

`str | None` means either string or `None`. Check it before string operations:

```python
name = find_name(2)
if name is not None:
    print(name.upper())
```

The condition narrows the static type.

## Prefer abstract input types when appropriate

If a function only iterates, accepting any iterable is more flexible:

```python
from collections.abc import Iterable

def total_length(words: Iterable[str]) -> int:
    return sum(len(word) for word in words)
```

Return a concrete type when callers rely on concrete behavior.

## Callable and aliases

```python
from collections.abc import Callable
from typing import TypeAlias

Transformer: TypeAlias = Callable[[str], str]

def apply(text: str, transform: Transformer) -> str:
    return transform(text)
```

An alias gives a complex type a domain name. It does not create a distinct runtime type.

## Annotate variables only when useful

```python
scores: dict[str, int] = {}
```

Inference already understands obvious initialized values. Add an annotation when an empty collection, public contract, or wider intended type needs clarity.

## Any is an escape hatch

`Any` tells a checker to allow operations without normal checking. It is useful at some dynamic boundaries but can spread and remove protection. Prefer `object` when a value is truly unknown and must be checked before use.

## Static checks and runtime checks solve different problems

- Type checker: finds inconsistent code paths before execution.
- Runtime validation: rejects malformed JSON, user input, database rows, and network data.
- Tests: verify selected behavior and edge cases.

Use all three at their correct boundaries.

## Check your understanding

You are ready when you can annotate optional and collection types and explain why a hint does not sanitize user input.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
