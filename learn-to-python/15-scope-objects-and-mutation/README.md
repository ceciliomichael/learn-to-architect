# Module 15: Names, Scope, Objects, and Mutation

## What you will learn

You will predict name lookup, object sharing, argument behavior, and mutation across function boundaries.

## Python looks through scopes

The useful LEGB summary is local, enclosing, global, built-in.

```python
tax_rate = 0.08

def total(price):
    fee = 2
    return price * (1 + tax_rate) + fee
```

`price` and `fee` are local. `tax_rate` is global. `print` and `len` are built-ins.

Reading a global is possible, but hidden dependencies make tests and reuse harder. Prefer explicit parameters.

## Assignment makes a name local

```python
count = 0

def broken():
    count = count + 1
```

Because the function assigns `count`, Python treats it as local, but its right side tries to read it before local assignment. This raises `UnboundLocalError`.

`global` can declare rebinding of a module-level name, and `nonlocal` can rebind an enclosing function name. Use them sparingly. Returning a new value is usually clearer.

## Arguments share object references

```python
def add_task(tasks):
    tasks.append("review")

items = ["read"]
add_task(items)
print(items)
```

The parameter and caller name refer to the same list, so mutation is visible.

Rebinding the local parameter does not rebind the caller:

```python
def replace_tasks(tasks):
    tasks = ["new"]
```

Python uses object sharing, sometimes described as call by sharing. It is not a simple pass-by-reference rule for variable names.

## Prefer clear side-effect contracts

Either state that a function mutates its argument:

```python
def sort_in_place(values):
    values.sort()
```

Or return a new object:

```python
def sorted_copy(values):
    return sorted(values)
```

Do not make callers guess.

## Identity and equality

`a == b` asks whether values are equal. `a is b` asks whether both names refer to the same object. Use identity for `None` and rare identity-specific logic, not ordinary value comparison.

## Copy to the needed depth

Shallow copies separate the outer container. `copy.deepcopy` recursively copies supported nested content, but can be expensive or wrong for shared resources. Design ownership explicitly instead of copying automatically.

## Check your understanding

You are ready when you can predict mutation versus rebinding and trace a name through local, enclosing, global, and built-in scopes.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
