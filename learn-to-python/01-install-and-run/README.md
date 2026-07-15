# Module 01: Install Python and Run a Program

## What you will learn

You will check Python, use the interactive prompt, run a script, and read a simple error.

## Check the interpreter

In a terminal:

```text
python --version
```

The result should be Python 3.12 or newer. On Windows, `py --version` may select the Python launcher. Use the same command consistently throughout a project.

The interpreter is the program that reads and executes Python code.

## Try the interactive prompt

Run `python`. At the `>>>` prompt, type:

```python
print("Hello, Python!")
```

`print` displays a value. Parentheses contain the value passed to it. Quotation marks create text.

Exit with:

```python
exit()
```

The prompt is useful for small experiments. Programs belong in files so they can be saved, reviewed, and tested.

## Run a script

Create `python-course-practice/01/hello.py` in a plain text editor:

```python
print("Hello, Python!")
print("I ran a saved program.")
```

From that folder:

```text
python hello.py
```

Python normally executes a script from top to bottom.

## Comments and indentation

```python
# This line explains the code and is not executed.
print("Visible")
```

Leading spaces have meaning in Python. Do not add indentation at the top level without a construct that requires a block. Later conditions, loops, functions, and classes use four spaces per level.

## Read a traceback

Temporarily add:

```python
print(missing_name)
```

The final traceback line reports `NameError` and explains that the name is not defined. The lines above show where it occurred. Errors are evidence. Read the exception type, message, file, and line before changing code.

Remove the failing line and run the script again.

## Common mistakes

- Running from the wrong folder: print the terminal location and list files.
- Saving as `hello.py.txt`: enable visible file extensions.
- Naming a file `random.py`, `json.py`, or another library name: it can hide the real module later.
- Copying smart quotes from rich text: Python source needs ordinary quotes.

## Check your understanding

You are ready when you can run the same two-line script twice and identify the exception type and line number in a traceback.
