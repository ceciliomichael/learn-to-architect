# Module 22 Exercises

Write and run Python programs. Keep a brief design note for the independent exercise.

## Warm-up: Change a working function

Start with:

```python
def double(n):
    return n * 2


print(double(5))
```

1. Add a function `triple(n)` that returns `n * 3`.
2. Print `triple(5)`.
3. Write a `main` function that prints both results, then call `main()`.

## Guided exercise: Total of a list

1. Create a list of four prices: `10, 4, 7, 9`.
2. Write `def total_of(values):` that returns the sum.
3. Write `def average_of(values):` that uses `total_of` or its own loop.
4. Print total and average from `main`.

## Independent exercise: Product lookup program

Parallel lists:

```text
products: Pen, Notebook, Eraser
prices: 5, 25, 8
```

Requirements:

- Store the data in two lists.
- Write `find_index(items, target)` that returns the index or `-1`.
- In `main`, input a product name, find it, and print the price or `Product not found`.
- Test at least one found case and one not-found case.

## Debugging task

Fix this program:

```python
def find_index(items, target)
    for i in range(len(items))
        if items[i] == target:
            return i
    return -1

names = ["Ada", "Bea"]
print(find_index(names, "Bea"))
print(names[2])
```

## Completion checklist

- [ ] I defined and called functions with parameters and return values.
- [ ] I used lists and valid indexes.
- [ ] I implemented a linear search function.
- [ ] I used parallel lists carefully.
- [ ] I fixed syntax and index errors.

When you have made a real attempt, compare your work with the [exercise solutions](../answers/exercise/exercise-solutions.md).
