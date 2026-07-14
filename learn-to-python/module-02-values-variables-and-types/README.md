# Module 02: Values, Variables, and Types

## What you will learn

You will bind names to values, inspect types, reassign names, and represent an intentional absence.

## Values are objects

Python works with objects. Each object has a type and value. Built-in examples are:

```python
print(42)
print(3.5)
print("tea")
print(True)
print(None)
```

The types are `int`, `float`, `str`, `bool`, and `NoneType`.

## Assignment binds a name

```python
course_name = "Python"
lesson_count = 38
is_beginner = True

print(course_name)
```

`=` does not mean mathematical equality here. It binds the name on the left to the object produced on the right.

Inspect types:

```python
print(type(course_name))
print(type(lesson_count))
```

Use `type` to investigate while learning, not as a substitute for thoughtful validation.

## Names can be rebound

```python
score = 10
score = 12
print(score)
```

The name now refers to 12. Python variables do not have one permanently declared type:

```python
result = 10
result = "complete"
```

This is valid, but changing a name's meaning and type makes programs harder to understand. Use one clear purpose per name.

## Use valid, meaningful names

Names can contain letters, numbers, and underscores, but cannot start with a number. They are case-sensitive. Use lowercase words separated by underscores:

```python
item_price = 25
```

Do not replace built-ins with names such as `list`, `str`, or `print`.

## None means no value is present

```python
middle_name = None
```

`None` is one special object. Test its identity with:

```python
print(middle_name is None)
```

Use `is None`, not `== None`. It means the absence is intentional, not empty text or zero.

## Assignment is not display

```python
total = 5 + 7
```

Scripts do not display assignment results automatically. Use `print(total)` when output is part of the program.

## Common mistakes

- Using a name before assignment causes `NameError`.
- Writing `True` or `None` in lowercase causes `NameError`.
- Putting a variable name in quotes prints the literal name, not its value.
- Reusing one name for unrelated meanings hides mistakes.

## Check your understanding

You are ready when you can explain assignment as name binding and distinguish `None`, zero, and empty text.
