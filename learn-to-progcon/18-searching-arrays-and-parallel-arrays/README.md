# Module 18: Searching Arrays and Parallel Arrays

## Before you start

Complete Modules 01 to 17. You should be comfortable with arrays, indexes, loops, selection, and flags (true/false values used as markers).

## What you will learn

- search an array with a linear search
- use a found flag and a found index
- keep related data aligned with parallel arrays
- replace some nested decision trees with data lookup
- update parallel arrays without breaking alignment

## Why this matters

Programs often ask: "Is this student in the list?" or "What price belongs to this product code?" Searching answers the first kind of question. Parallel arrays answer the second by keeping two lists lined up by index.

## 1. Linear search

A **linear search** checks array elements one by one from the start until it finds the target or runs out of elements.

Design idea:

```text
SET names = ["Ana", "Ben", "Cara", "Dan"]
INPUT target
SET found = false
SET foundIndex = -1
SET index = 0

WHILE index < 4 AND found == false
    IF names[index] == target THEN
        SET found = true
        SET foundIndex = index
    ELSE
        SET index = index + 1
    END IF
END WHILE

IF found == true THEN
    OUTPUT target "found at index" foundIndex
ELSE
    OUTPUT target "not found"
END IF
```

A **found flag** is a boolean that becomes true when the search succeeds. Storing `foundIndex` remembers where the match was.

The condition `index < 4 AND found == false` stops early after a match. You can also always scan the whole array. Early exit is often clearer for beginners once the control variable updates carefully.

## 2. Trace a search

Search for `"Cara"` in `["Ana", "Ben", "Cara", "Dan"]`.

| Step | index | names[index] | found | foundIndex |
| --- | --- | --- | --- | --- |
| start | 0 | Ana | false | -1 |
| compare | 0 | Ana | false | -1 |
| next | 1 | Ben | false | -1 |
| next | 2 | Cara | true | 2 |

The loop stops. Output reports index `2`.

If the target is `"Eve"`, every comparison fails and `found` stays false.

## 3. Parallel arrays

**Parallel arrays** are two or more arrays whose elements at the same index belong together.

Example:

```text
SET products = ["Tea", "Bread", "Milk"]
SET prices   = [3.5,  2.0,   1.5]
```

Meaning:

| index | products[index] | prices[index] |
| --- | --- | --- |
| 0 | Tea | 3.5 |
| 1 | Bread | 2.0 |
| 2 | Milk | 1.5 |

`products[1]` and `prices[1]` are one pair: Bread costs 2.0.

Parallel arrays must stay the same length and keep matching order. If you insert a product at index 1, you must also insert its price at index 1.

## 4. Lookup with parallel arrays

Problem: user enters a product name; program outputs the price.

```text
SET products = ["Tea", "Bread", "Milk"]
SET prices   = [3.5,  2.0,   1.5]
INPUT name
SET found = false
SET index = 0

WHILE index < 3 AND found == false
    IF products[index] == name THEN
        OUTPUT "Price:" prices[index]
        SET found = true
    ELSE
        SET index = index + 1
    END IF
END WHILE

IF found == false THEN
    OUTPUT "Product not found"
END IF
```

The search runs on `products`. The answer is read from `prices` at the same index.

## 5. Replacing nested decisions with data

A long chain of decisions:

```text
IF code == "A1" THEN
    OUTPUT 10
ELSE IF code == "B2" THEN
    OUTPUT 12
ELSE IF code == "C3" THEN
    OUTPUT 8
...
END IF
```

can become arrays plus a search:

```text
SET codes = ["A1", "B2", "C3"]
SET costs = [10, 12, 8]
```

Data is easier to extend. Adding a new code means adding one element to each array, not writing another nested branch.

Selection is still needed for "found or not found." The point is that the growing list of cases lives in data, not in deeper and deeper decisions.

## 6. Keeping parallel arrays consistent

When you update related data, update every parallel array at the same index.

Bad:

```text
SET products[1] = "Roll"
// forgot to change prices[1]
```

Good:

```text
SET products[1] = "Roll"
SET prices[1] = 2.25
```

When you think of "one record," think of "one index across all parallel arrays."

## Predict the result

```text
SET ids = [101, 102, 103]
SET seats = ["A", "B", "C"]
```

A search finds `102` at index `1`. What seat letter belongs with that id?

Expected answer: `"B"`, because `seats[1]` pairs with `ids[1]`.

## Common mistakes

### Stopping the loop incorrectly

If you set `found = true` but still increment index in a confusing way, traces get messy. Prefer a clear loop condition that includes `found == false`, or use a FOR loop that sets a flag and breaks out in languages that support break. In pseudocode, early-exit WHILE is fine when written carefully.

### Searching one array and reading a different index from another

Always use the same index for parallel data.

### Assuming the item exists

Always handle the not-found case.

### Letting parallel arrays grow to different lengths

If one array has 5 items and the other has 4, some indexes no longer form valid pairs.

## Check your understanding

1. What does a linear search do?
2. What is a found flag for?
3. What makes two arrays parallel?
4. If `names[2]` is `"Sam"` and `scores` is parallel, where is Sam's score?
5. Why can parallel arrays replace some long IF/ELSE IF chains?

## Practice

Complete the [module exercises](./exercise/exercise.md). Then take the [module quiz](./quiz/quiz.md).

## Next step

In [Module 19](../19-processing-arrays-with-loops/README.md), you will process every array element for totals, averages, minimums, and maximums.
