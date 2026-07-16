# Module 06 Quiz Answers

## Answer 1

A **variable** is named storage whose value can change during the solution. Example: `total` grows as each item price is added.

A **constant** is a named value that should stay fixed for the whole run. Example: `TAX_RATE = 0.08` for a fixed tax percentage in the problem.

## Answer 2

Step by step:

1. `x = 2`
2. `y = 5`
3. `x = x + y` becomes `x = 2 + 5`, so `x = 7`
4. `y = x` copies 7 into `y`, so `y = 7`

Final values: `x` is 7, `y` is 7.

## Answer 3

- `studentName` is better than `n` because it states the meaning.
- `itemPrice` is better than `item price` because names cannot contain spaces.
- Separate names `moneyTotal` and `attendCount` are better than reusing `total` for two unrelated meanings. One name should keep one job.

## Answer 4

- `"B+"` is **text**
- `88` is a **number**
- `false` is **yes/no**
- `"false"` is **text** (characters inside quotes, not a true yes/no value)

## Answer 5

`average` is computed before `total` and `count` are set. The right side uses names that do not yet have values.

Fixed order:

```text
SET total = 90
SET count = 3
SET average = total / count
DISPLAY average
```

Now the displayed average is `30`.
