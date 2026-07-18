# Module 29: Iterators and Generators

## What you will learn

You will understand the iteration protocol and produce lazy sequences with generator functions.

## Iterable and iterator are different roles

An iterable can produce an iterator. An iterator produces one item at a time and remembers progress.

```python
values = [10, 20]
iterator = iter(values)
print(next(iterator))
print(next(iterator))
```

Another `next` raises `StopIteration`. A for loop handles this protocol automatically.

Calling `iter` on a list creates a fresh iterator. Calling `iter` on an iterator normally returns the same iterator, so it remains single-use.

## A generator function uses yield

```python
def countdown(start: int):
    current = start
    while current > 0:
        yield current
        current -= 1
```

Calling `countdown(3)` returns a generator without running the full body. Each `next` resumes until the next `yield`. Local state remains suspended between values.

## Return ends a generator

Reaching `return` or the function end raises `StopIteration` to the consumer. A returned value can be carried by StopIteration for delegation use, but ordinary for loops ignore it.

Do not explicitly raise `StopIteration` inside a generator to end it. Use `return`.

## Delegate with yield from

```python
def all_numbers():
    yield from range(3)
    yield from range(3, 6)
```

`yield from` delegates iteration and advanced send, throw, close behavior to a subiterator.

## Cleanup and close

A generator can use `try/finally` for cleanup. Calling `close` raises `GeneratorExit` at the suspended point. Consumers should close generators that own resources, but a context manager is usually a clearer resource boundary than a long-lived generator.

## Laziness tradeoffs

Generators can process streams with bounded memory and stop early. They are single-use, may delay failures until consumption, and can keep resources or references alive while suspended.

## Check your understanding

You are ready when you can trace `iter`, `next`, `yield`, suspension, exhaustion, and a second attempt to consume the same iterator.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
