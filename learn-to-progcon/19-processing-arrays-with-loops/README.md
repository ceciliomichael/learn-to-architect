# Module 19: Processing Arrays with Loops

## Before you start

Complete Modules 01 to 18. You should know array indexes, FOR and WHILE loops, accumulators, and parallel arrays.

## What you will learn

- process every element of an array with a FOR loop
- compute sum, average, minimum, and maximum
- display all values cleanly
- handle a partially filled array with a logical size
- write pseudocode and a simple flowchart for array processing

## Why this matters

Storing values in an array is only half the job. Real tasks ask for totals, averages, highest scores, and printed lists. Loops turn a whole collection into one useful result.

## 1. Visit every element

For an array of size `n` with 0-based indexes, a counted loop from `0` to `n - 1` visits each element once.

```text
SET scores = [80, 90, 70, 85]
FOR index FROM 0 TO 3 STEP 1
    OUTPUT scores[index]
END FOR
```

Output:

```text
80
90
70
85
```

## 2. Sum and average

An **accumulator** holds a running total.

```text
SET scores = [80, 90, 70, 85]
SET total = 0
FOR index FROM 0 TO 3 STEP 1
    SET total = total + scores[index]
END FOR
SET average = total / 4
OUTPUT total
OUTPUT average
```

Trace idea:

| index | scores[index] | total after add |
| --- | --- | --- |
| 0 | 80 | 80 |
| 1 | 90 | 170 |
| 2 | 70 | 240 |
| 3 | 85 | 325 |

Average is `325 / 4 = 81.25`.

Initialize the accumulator before the loop. If you forget `SET total = 0`, the total is undefined.

## 3. Minimum and maximum

To find the highest value:

1. Set `maximum` to the first element.
2. Loop through the remaining elements.
3. Whenever you see a larger value, update `maximum`.

```text
SET scores = [80, 90, 70, 85]
SET maximum = scores[0]
FOR index FROM 1 TO 3 STEP 1
    IF scores[index] > maximum THEN
        SET maximum = scores[index]
    END IF
END FOR
OUTPUT maximum
```

Expected maximum: `90`.

Minimum uses `<` instead of `>`.

Starting from `scores[0]` avoids a fake starter such as `0`, which would fail for all-negative numbers.

## 4. Partial fills and logical size

Sometimes an array can hold up to 100 values, but the user only entered 6 values today.

- **Physical size**: how many slots the array can hold (capacity).
- **Logical size**: how many slots currently hold useful data.

Design with a logical size variable:

```text
// capacity is 5, but only count values are used
SET values = [0, 0, 0, 0, 0]
SET count = 0

// later, after inputs:
// values[0]..values[count-1] are valid

SET total = 0
FOR index FROM 0 TO count - 1 STEP 1
    SET total = total + values[index]
END FOR
```

Always loop to `count - 1`, not to the full capacity, when only part of the array is filled.

## 5. Flowchart shape for array processing

```text
        [START]
           |
    [SET total = 0]
           |
    [SET index = 0]
           |
          / \
         /   \ index <= last?
         \   /
          \ /
      yes |   \ no
          |    \
   [total = total + array[index]]
          |
   [index = index + 1]
          |
          +-----> back to decision
                   |
                [OUTPUT total]
                   |
                 [END]
```

The same pattern supports average (divide after the loop), display (OUTPUT inside the loop), and min/max (compare inside the loop).

## 6. Combine skills carefully

Example: print all scores, then print average and highest.

```text
SET scores = [80, 90, 70, 85]
SET total = 0
SET maximum = scores[0]

FOR index FROM 0 TO 3 STEP 1
    OUTPUT scores[index]
    SET total = total + scores[index]
    IF scores[index] > maximum THEN
        SET maximum = scores[index]
    END IF
END FOR

SET average = total / 4
OUTPUT "Average:" average
OUTPUT "Highest:" maximum
```

One loop can do several jobs if each job fits the same visit order. If the logic becomes hard to read, use separate loops. Clarity matters more than squeezing everything into one pass.

## Predict the result

```text
SET nums = [4, 1, 9, 2]
SET minimum = nums[0]
FOR index FROM 1 TO 3 STEP 1
    IF nums[index] < minimum THEN
        SET minimum = nums[index]
    END IF
END FOR
OUTPUT minimum
```

Expected output: `1`

## Common mistakes

### Dividing by the wrong count

Average uses the number of values included, not a random constant.

### Starting max or min at 0

Use the first real element instead.

### Looping past the logical size

Extra unused slots can corrupt totals.

### Updating the accumulator only outside the loop

Each element must be added inside the loop body.

## Check your understanding

1. What is an accumulator used for when processing an array?
2. Why is `maximum = scores[0]` a good starting choice?
3. What is the difference between physical size and logical size?
4. After summing 5 values into `total`, how do you get the average?
5. Can one FOR loop both print elements and compute a total? When might two loops be clearer?

## Practice

Complete the [module exercises](./exercise/exercise.md). Then take the [module quiz](./quiz/quiz.md).

## Next step

In [Module 20](../20-python-setup-and-first-programs/README.md), you will run Python and begin turning designs into real programs.
