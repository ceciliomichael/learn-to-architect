# Module 17: Arrays, Indexes, and the Storage Model

## Before you start

Complete Modules 01 to 16. You should already know variables, loops, selection, modules, pseudocode, flowcharts, and trace tables.

This module still focuses on design. You will use array ideas in pseudocode and plain diagrams. Python lists appear later.

## What you will learn

By the end of this module, you will be able to:

- explain what an array is and why programs use arrays
- state an array size and identify a valid index
- read and write one element with `array[index]` notation
- use a row-of-slots model to trace related values without making claims about a language's physical memory layout
- redesign a problem that would otherwise need many separate variables

## Why this matters

A teacher may store twenty quiz scores. A shop may store seven daily totals. Writing `score1`, `score2`, ... `score20` is clumsy and hard to loop over. An array stores many related values under one name and lets a loop visit each value by position.

## 1. What an array is

An **array** is a named, indexed collection of values stored in order. Many languages require every element to have the same type. Some collections, including Python lists, can technically mix types. This course keeps elements the same kind because loops, comparisons, totals, and searches are clearer and safer that way.

Examples:

- an array of five temperatures
- an array of ten student names
- an array of seven daily sales amounts

Each single value inside the array is an **element**.

In design notation, you can declare an array like this:

```text
DECLARE scores AS array of 5 numbers
```

Or, after values are known:

```text
SET scores = [88, 92, 75, 90, 84]
```

The square brackets show an ordered list of values. The whole collection is still one named array: `scores`.

## 2. Size and indexes

The **size** of an array is how many elements it can hold.

For five scores, the size is 5.

An **index** is the position number used to select one element.

This course uses **0-based indexes**. That means:

- the first element is at index `0`
- the second element is at index `1`
- the last element of a size-5 array is at index `4`

Valid indexes for size 5 are `0`, `1`, `2`, `3`, and `4`.

Why start at 0? Many programming languages, including Python, use 0-based indexes. Learning that convention now makes later translation smoother.

Some textbooks use 1-based indexes. If you read a design that starts at 1, adjust carefully. In this course, assume 0-based unless a lesson says otherwise.

## 3. The storage model used in this course

For design and tracing, draw an array as a row of labeled slots:

```text
scores:
 index:   0     1     2     3     4
       +-----+-----+-----+-----+-----+
 value | 88  | 92  | 75  | 90  | 84  |
       +-----+-----+-----+-----+-----+
```

Each drawn slot represents one element. Neighboring indexes mean neighboring positions in the collection's logical order.

This is an abstract model, not a promise that every value object sits beside the next value in physical memory. Languages implement collections differently. A low-level fixed-type array may place element data in one contiguous region. A Python list maintains an ordered collection of references, and the referenced objects can live elsewhere. The useful idea for this course is independent of those details: an array name plus a valid index selects one element.

## 4. Reading an element

To read one element, write the array name and the index in brackets:

```text
SET firstScore = scores[0]
OUTPUT firstScore
```

If `scores` holds `[88, 92, 75, 90, 84]`, then `scores[0]` is `88` and `scores[2]` is `75`.

A loop can visit every element:

```text
FOR index FROM 0 TO 4 STEP 1
    OUTPUT scores[index]
END FOR
```

## 5. Writing an element

Assignment can store a new value into one slot:

```text
SET scores[1] = 95
```

Only index `1` changes. The other elements stay the same.

```text
Before: [88, 92, 75, 90, 84]
After:  [88, 95, 75, 90, 84]
```

## 6. Arrays beat many separate variables

Compare these two designs for three prices:

```text
SET price1 = 10
SET price2 = 4
SET price3 = 7
SET total = price1 + price2 + price3
```

```text
SET prices = [10, 4, 7]
SET total = 0
FOR index FROM 0 TO 2 STEP 1
    SET total = total + prices[index]
END FOR
```

For three values, either approach works. For thirty values, the array plus loop stays short and clear. The same loop body works no matter how many elements you process, as long as the stop index matches the array size.

## 7. Safe index habits

Always keep indexes inside the valid range.

For an array of size `n`, valid indexes are `0` through `n - 1`.

Common mistakes:

- using index `n` for a size-`n` array
- forgetting that the first item is at `0`
- mixing up the index with the value stored at that index

Example:

```text
SET temps = [21, 19, 23]
OUTPUT temps[1]
```

The output is `19`, not `1`. The index is the position. The value is what sits in that position.

## Predict the result

Array:

```text
SET names = ["Ana", "Ben", "Cara"]
```

What does each line produce?

```text
OUTPUT names[0]
OUTPUT names[2]
SET names[1] = "Bea"
OUTPUT names[1]
```

Write your answers before checking.

Expected:

```text
Ana
Cara
Bea
```

## Common mistakes

### Treating the size as the last index

For size 5, the last valid index is 4, not 5.

### Using a separate variable when an array fits better

If values are the same kind and will be processed the same way, prefer one array.

### Confusing `scores[i]` with `i`

`i` is the position. `scores[i]` is the value at that position.

### Leaving the array empty in the design

If the problem needs five scores, show how those five values are input or set before you process them.

## Check your understanding

1. What is an element of an array?
2. For an array of size 8 with 0-based indexes, what is the first index and what is the last valid index?
3. If `prices = [5, 12, 9]`, what is `prices[2]`?
4. Why are arrays useful when a loop must process many related values?
5. Does changing `prices[0]` automatically change `prices[1]`?

## Practice

Complete the [module exercises](./exercise/exercise.md). Then take the [module quiz](./quiz/quiz.md).

## Next step

In [Module 18](../18-searching-arrays-and-parallel-arrays/README.md), you will search arrays and keep related data aligned with parallel arrays.
