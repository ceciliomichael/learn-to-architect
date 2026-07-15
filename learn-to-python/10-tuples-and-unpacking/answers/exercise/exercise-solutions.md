# Exercise Solutions: Tuples and Unpacking

```python
product = ("Notebook", 4.25, True)
name, price, in_stock = product
print(name, price, in_stock)

empty = ()
one_item = ("only",)
print(type(empty), len(empty))
print(type(one_item), len(one_item))

first, *middle, last = (1, 2, 3, 4, 5)
print(first, middle, last)

left = "west"
right = "east"
left, right = right, left
print(left, right)

record = ("Ava", [80, 90])
record[1].append(100)
print(record)
```

The tuple's second item still refers to the same list object. Mutating that object does not replace the tuple item.
