# Exercise Solutions: Values, Variables, and Types

```python
course_title = "Python Foundations"
module_number = 2
price = 19.95
is_available = True
optional_note = None

print(course_title, type(course_title))
print(module_number, type(module_number))
print(price, type(price))
print(is_available, type(is_available))
print(optional_note, type(optional_note))

module_number = module_number + 1
print(module_number)
print(optional_note is None)
```

Using `later_value` before `later_value = 5` raises `NameError`. Move the assignment before the use.
