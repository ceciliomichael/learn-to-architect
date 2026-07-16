# Module 18 Exercises

Use pseudocode and short trace notes. No Python required.

## Warm-up: Change a working search

Start with a search for a name in:

```text
SET names = ["Ira", "Jo", "Kai"]
```

1. Write a linear search for target `"Jo"`.
2. Change the target to `"Sam"` and show the not-found message path.
3. Add a `foundIndex` variable and output it when found.

## Guided exercise: Product price lookup

Parallel arrays:

```text
products: ["Pen", "Notebook", "Eraser", "Ruler"]
prices:   [5, 25, 8, 15]
```

Design a program that:

1. Inputs a product name.
2. Searches `products` with a linear search.
3. If found, outputs the matching price from `prices`.
4. If not found, outputs `Product not found`.

Then desk-check:

- target `Notebook` (expect price 25)
- target `Bag` (expect not found)

## Independent exercise: Attendance codes

A club stores:

```text
memberIds: [10, 11, 12, 13]
statuses:  ["Present", "Absent", "Present", "Late"]
```

Requirements:

- Input an id.
- Find it in `memberIds`.
- Output the matching status.
- If the id is missing, output `Unknown member`.
- Explain in one sentence why `statuses[i]` is safe only when `i` came from a successful search of `memberIds`.

## Debugging / desk-check task

This design has logic problems:

```text
SET cities = ["Manila", "Cebu", "Davao"]
SET codes  = ["MNL", "CEB", "DVO"]
INPUT city
SET index = 0
SET found = false
WHILE index < 3
    IF cities[index] == city THEN
        SET found = true
    END IF
    SET index = index + 1
END WHILE
IF found == true THEN
    OUTPUT codes[index]
ELSE
    OUTPUT "No code"
END IF
```

1. Why is `codes[index]` wrong after the loop?
2. Write a corrected design that prints the correct code for a found city.
3. Trace target `Cebu` on your corrected version.

## Completion checklist

- [ ] I wrote a linear search with a found flag.
- [ ] I used parallel arrays with matching indexes.
- [ ] I handled not-found cases.
- [ ] I desk-checked at least one successful search and one failed search.
- [ ] I fixed a post-loop index mistake.

When you have made a real attempt, compare your work with the [exercise solutions](../answers/exercise/exercise-solutions.md).
