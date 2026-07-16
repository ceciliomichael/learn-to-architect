# Module 23: Capstone Design and Build

## Before you start

Complete Modules 01 to 22. You should be able to design with algorithms, pseudocode, flowcharts, modules, selection, loops, and arrays, then implement those designs in Python with functions and lists.

## What you will learn

- choose a small project with a clear scope
- write requirements as inputs, processes, and outputs
- produce algorithm, pseudocode, flowchart, and hierarchy chart artifacts
- implement the design in Python
- test with a trace table and real runs
- present what you built in plain language

## Why this matters

Programming concepts become durable when you carry one problem all the way from idea to running program. This capstone is your proof that design and code belong together.

## 1. Pick a scoped problem

A good capstone is small enough to finish, but rich enough to use several course ideas.

Choose **one** project brief:

### Option A: Grade calculator

- Input several quiz scores (for example 3 to 5 scores).
- Output each score, the average, the highest score, and a pass/review message.
- Use a list, a loop, and at least two functions.

### Option B: Shop receipt with discount

- Input item prices until a sentinel such as `0`.
- Compute subtotal.
- If subtotal is at least a threshold, apply a discount percent.
- Output subtotal, discount amount, and final total.
- Use a loop, selection, and functions for discount calculation and printing.

### Option C: Attendance or quiz scorer

- Store parallel lists of names and statuses or scores.
- Let the user look up one name and see the matching status or score.
- Also print a count of present students or scores above a threshold.
- Use search, parallel lists, and functions.

If you invent your own project, keep the same size: a few inputs, clear rules, modular design, and testable outputs.

## 2. Write requirements first

Before coding, write:

1. **Problem statement**: one or two sentences.
2. **Inputs**: what the user provides.
3. **Processes**: calculations and decisions.
4. **Outputs**: what the program must show.
5. **Constraints**: sentinel values, valid ranges, number of items.

Example for Option A:

```text
Problem: Compute class quiz statistics and a pass message.
Inputs: three floating-point scores.
Processes: total, average, maximum, compare average to 75.
Outputs: scores list, average, maximum, Pass or Review.
```

## 3. Produce design artifacts

Create these on paper or in text files:

1. **Algorithm**: numbered steps in plain language.
2. **Pseudocode**: full design with modules.
3. **Hierarchy chart**: main and helper modules.
4. **Flowchart**: at least the main control path (sequence, decisions, loops).
5. **Trace table**: one normal case and one edge case.

Do not skip design because you already know Python. The point of ProgCon is deliberate design.

## 4. Implement in Python

Translate structure first:

1. Create empty functions matching the hierarchy chart.
2. Implement helpers.
3. Implement `main`.
4. Run with the same sample data used in your trace table.
5. Compare program output with the trace expectations.

If the outputs disagree, fix the design or the translation. Do not only patch randomly.

## 5. Test with evidence

Minimum test set:

| Case | Purpose |
| --- | --- |
| Normal case | typical valid inputs |
| Boundary case | exact threshold, such as average 75 |
| Edge case | empty list if allowed, or single item, or not-found search |

Record:

- inputs
- expected results from the trace
- actual program output
- pass or fail

## 6. Present your work

Write a short presentation note (half a page is enough):

1. Which project option you chose and why
2. What modules/functions you used
3. One design decision that made the program clearer
4. One bug you found with a trace or test, and how you fixed it
5. What you would add next if you had more time

## 7. Sample skeleton (Option A shape)

```python
def read_scores(count):
    scores = []
    for i in range(count):
        value = float(input("Score: "))
        scores.append(value)
    return scores


def average_of(scores):
    total = 0.0
    for score in scores:
        total = total + score
    return total / len(scores)


def maximum_of(scores):
    highest = scores[0]
    for score in scores:
        if score > highest:
            highest = score
    return highest


def main():
    scores = read_scores(3)
    avg = average_of(scores)
    high = maximum_of(scores)
    print("Scores:", scores)
    print("Average:", avg)
    print("Highest:", high)
    if avg >= 75:
        print("Pass")
    else:
        print("Review")


main()
```

Your project may differ. The skeleton shows modular shape, not the only correct program.

## Common mistakes

### Choosing a huge project

A social network clone is too large. Finish a small tool well.

### Coding with no requirements

If inputs and outputs are fuzzy, every feature becomes a debate.

### Design that does not match the code

Update both when you change the approach.

### Testing only the happy path

Boundary and not-found cases catch many logic errors.

## Check your understanding

1. What four design artifacts should your capstone include?
2. Why write requirements before code?
3. What is one boundary case for a pass mark of 75?
4. How do a trace table and a program run work together?
5. What belongs in a short project presentation note?

## Practice

Complete the [module exercises](./exercise/exercise.md). Then take the [module quiz](./quiz/quiz.md).

## Next step

You have finished Learn Programming Concepts. To go deeper with the Python language itself, continue with [Learn Python](../../learn-to-python/README.md). Your ProgCon design habits will transfer directly.
