# Module 22 Exercise Solutions

## Warm-up solution

```python
def double(n):
    return n * 2


def triple(n):
    return n * 3


def main():
    print(double(5))
    print(triple(5))


main()
```

Expected output:

```text
10
15
```

## Guided exercise solution

```python
def total_of(values):
    total = 0
    for value in values:
        total = total + value
    return total


def average_of(values):
    return total_of(values) / len(values)


def main():
    prices = [10, 4, 7, 9]
    print("Total:", total_of(prices))
    print("Average:", average_of(prices))


main()
```

Expected: total `30`, average `7.5`.

## Independent exercise solution

```python
def find_index(items, target):
    index = 0
    while index < len(items):
        if items[index] == target:
            return index
        index = index + 1
    return -1


def main():
    products = ["Pen", "Notebook", "Eraser"]
    prices = [5, 25, 8]
    name = input("Product: ")
    position = find_index(products, name)
    if position == -1:
        print("Product not found")
    else:
        print("Price:", prices[position])


main()
```

Found example: `Notebook` prints `Price: 25`. Missing example: `Bag` prints `Product not found`.

## Debugging task solution

```python
def find_index(items, target):
    for i in range(len(items)):
        if items[i] == target:
            return i
    return -1


names = ["Ada", "Bea"]
print(find_index(names, "Bea"))
print(names[1])
```

Fixes:

1. Added `:` after the `def` line and the `for` line.
2. Replaced invalid `names[2]` with `names[1]` (last valid index).
