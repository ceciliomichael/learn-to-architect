# Module 20: Python Setup and First Programs

## Before you start

Complete Modules 01 to 19. You should be able to write sequential designs in pseudocode and check them with a trace table.

You need a way to run Python. See the [course guide setup section](../README.md#for-python-work-modules-20-to-23).

## What you will learn

- explain the purpose of an editor or IDE
- run a Python program online or on your computer
- print text with `print`
- leave notes with comments
- tell source code apart from program output
- read a simple error message
- convert a tiny sequential design into Python

## Why this matters

Design skills are the foundation. Running code is how you see a finished design work on a real machine. Python is a popular language with clear syntax for beginners, so it is a good first implementation language for ProgCon.

## 1. Editors, IDEs, and the interpreter

An **editor** is a program for writing text files, including code.

An **IDE** (integrated development environment) is an editor plus helpful tools such as run buttons, error highlighting, and file browsers.

The **Python interpreter** reads your Python file and carries out the instructions.

You can write code in a simple editor and run it from a terminal, use an IDE, or use an online compiler. All three are programming environments. The user of a finished app usually never sees that environment.

## 2. Check Python on your computer

In a terminal:

```text
python --version
```

On some Windows systems:

```text
py --version
```

Install a current stable Python 3 release from <https://www.python.org>. As of July 2026, the current stable feature series is Python 3.14. The course examples also work with supported Python 3.12 and 3.13 releases. Avoid preview or beta releases while learning unless you intentionally want to test an upcoming version.

## 3. Your first program

Create a file named `hello.py`:

```python
print("Hello, ProgCon!")
```

Run it:

```text
python hello.py
```

Output:

```text
Hello, ProgCon!
```

`print` displays a value. The parentheses hold what you want to display. Quotation marks create text, also called a **string**.

## 4. Programs run from top to bottom

```python
print("First")
print("Second")
print("Third")
```

Output:

```text
First
Second
Third
```

For now, treat Python like your sequence designs: start at the top and move down one statement at a time.

## 5. Comments

Comments are notes for people. Python ignores them when the program runs.

```python
# This program greets the learner.
print("Welcome")
```

A full-line comment starts with `#`.

## 6. Source code vs output

Source:

```python
print("Tea")
```

Output:

```text
Tea
```

Quotation marks and parentheses are part of the source. They are not part of this output.

## 7. Reading simple errors

### SyntaxError

```python
print("Missing end
```

Python reports a **SyntaxError** when the code breaks language rules, such as an unfinished string.

### NameError

```python
print(message)
```

If `message` was never created, Python reports a **NameError**.

Read the final error type and message first, then the file name and line number. Fix the first real problem before chasing later messages.

## 8. Translate a tiny sequential design

Pseudocode:

```text
START
    OUTPUT "Shop total"
    SET price = 12
    SET tax = 2
    SET total = price + tax
    OUTPUT total
END
```

Python:

```python
print("Shop total")
price = 12
tax = 2
total = price + tax
print(total)
```

Output:

```text
Shop total
14
```

Notice the mapping:

| Design idea | Python idea in this module |
| --- | --- |
| OUTPUT text | `print("...")` |
| SET name = value | `name = value` |
| top to bottom | top to bottom |

You will learn decisions, loops, functions, and lists in the next modules. Keep designs nearby while you code.

## Predict the result

```python
print("A")
# print("B")
print("C")
```

Expected output:

```text
A
C
```

## Common mistakes

### Saving as `hello.py.txt`

Turn on file extensions and confirm the name ends with `.py`.

### Running in the wrong folder

If Python cannot find the file, check the terminal's current folder.

### Curved quotation marks from rich text

Code needs straight quotes: `"text"`.

### Expecting comments to print

Comments never become output.

## Check your understanding

1. What does the Python interpreter do?
2. What is the difference between source code and output?
3. Does a line starting with `#` run?
4. What kind of error is an unfinished string likely to cause?
5. How do you write design `OUTPUT "Hi"` in Python?

## Practice

Complete the [module exercises](./exercise/exercise.md). Then take the [module quiz](./quiz/quiz.md).

## Next step

In [Module 21](../21-translating-design-to-python-control-flow/README.md), you will translate variables, input, decisions, and loops from design into Python.
