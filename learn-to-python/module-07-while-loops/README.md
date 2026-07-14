# Module 07: Repeat with While Loops

## What you will learn

You will repeat while a condition remains true and design a clear termination path.

## A while loop rechecks its condition

```python
count = 1
while count <= 3:
    print(count)
    count += 1
```

The loop needs initial state, a condition, and progress toward termination. Forgetting `count += 1` creates an infinite loop. Interrupt a terminal program with Ctrl+C.

## Validate a simple menu

```python
choice = ""
while choice != "1" and choice != "2" and choice != "q":
    choice = input("Choose 1, 2, or q: ").strip().lower()

print(f"You chose {choice}")
```

The loop works with strings, so invalid number conversion is not involved.

## Break and continue

`break` exits the nearest loop:

```python
while True:
    command = input("Command or quit: ").strip().lower()
    if command == "quit":
        break
    if not command:
        continue
    print(f"Running {command}")
```

`continue` begins the next iteration. Keep both rare and clear. A meaningful condition is often easier to understand than several exits.

## Loop else

An optional `else` runs when the loop ends normally, but not after `break`:

```python
attempts = 0
while attempts < 3:
    if input("Code: ") == "open":
        print("Accepted")
        break
    attempts += 1
else:
    print("No attempts remain")
```

## Numeric validation without exceptions yet

```python
text = input("Nonnegative whole number: ").strip()
while not text.isdecimal():
    text = input("Use digits only: ").strip()
number = int(text)
```

This deliberately accepts only nonnegative decimal digits. Module 17 uses exceptions for broader numeric forms.

## Check your understanding

You are ready when you can identify initialization, condition, progress, and termination for a loop.
