# Module 21 Exercises

Write and run Python programs. Keep a short pseudocode note above each independent solution.

## Warm-up: Change a working decision

Start with:

```python
temperature = 31
if temperature > 30:
    print("Hot day")
else:
    print("Mild day")
```

1. Change the threshold to 25 and test with `temperature = 24`.
2. Add an `elif` branch for temperatures above 35 that prints `Extreme heat`.
3. Confirm only one message prints for each test value you try.

## Guided exercise: Ticket check

Design:

```text
INPUT age
IF age < 13 THEN
    OUTPUT "Child ticket"
ELSE IF age <= 59 THEN
    OUTPUT "Adult ticket"
ELSE
    OUTPUT "Senior ticket"
END IF
```

1. Translate to Python using `input` and `int`.
2. Test with ages 10, 30, and 65.
3. Write the expected message beside each test in a comment.

## Independent exercise: Average and pass message

Write a program that:

1. Reads three numbers (floats are fine).
2. Prints their average.
3. Prints `Pass` if the average is at least 75, otherwise `Needs review`.
4. Uses a `for` loop with `range(3)` to read the three values.

## Debugging task

Fix the program:

```python
count = 1
while count <= 3
print(count)
count = count + 1

score = input("Score: ")
if score >= 50:
    print("OK")
```

Issues include punctuation, indentation, and type conversion.

## Completion checklist

- [ ] I used assignment, input conversion, and arithmetic.
- [ ] I wrote if/elif/else with correct colons and indentation.
- [ ] I wrote a while loop that terminates.
- [ ] I used for and range for counted work.
- [ ] I fixed a mixed syntax and type bug.

When you have made a real attempt, compare your work with the [exercise solutions](../answers/exercise/exercise-solutions.md).
