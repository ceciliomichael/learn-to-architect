# Module 18 Exercise Solutions

## Warm-up solution

```text
SET names = ["Ira", "Jo", "Kai"]
INPUT target
SET found = false
SET foundIndex = -1
SET index = 0

WHILE index < 3 AND found == false
    IF names[index] == target THEN
        SET found = true
        SET foundIndex = index
    ELSE
        SET index = index + 1
    END IF
END WHILE

IF found == true THEN
    OUTPUT target "found at" foundIndex
ELSE
    OUTPUT target "not found"
END IF
```

For `"Jo"`, output is found at index `1`. For `"Sam"`, output is not found.

## Guided exercise solution

```text
SET products = ["Pen", "Notebook", "Eraser", "Ruler"]
SET prices   = [5, 25, 8, 15]
INPUT name
SET found = false
SET index = 0

WHILE index < 4 AND found == false
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

Desk-check `Notebook`: match at index 1, price 25. Desk-check `Bag`: no match, not found message.

## Independent exercise solution

```text
SET memberIds = [10, 11, 12, 13]
SET statuses  = ["Present", "Absent", "Present", "Late"]
INPUT id
SET found = false
SET index = 0

WHILE index < 4 AND found == false
    IF memberIds[index] == id THEN
        OUTPUT statuses[index]
        SET found = true
    ELSE
        SET index = index + 1
    END IF
END WHILE

IF found == false THEN
    OUTPUT "Unknown member"
END IF
```

`statuses[i]` is safe only when `i` is an index where `memberIds[i]` matched the input. Otherwise `i` does not refer to that member's row.

## Debugging / desk-check task solution

1. After the WHILE loop finishes, `index` has been increased until it is `3`. Index `3` is outside the valid range `0..2`, so `codes[index]` is invalid. Even if the city was found earlier, the design never saved the matching index.

2. Corrected design:

```text
SET cities = ["Manila", "Cebu", "Davao"]
SET codes  = ["MNL", "CEB", "DVO"]
INPUT city
SET index = 0
SET found = false
SET foundIndex = -1

WHILE index < 3 AND found == false
    IF cities[index] == city THEN
        SET found = true
        SET foundIndex = index
    ELSE
        SET index = index + 1
    END IF
END WHILE

IF found == true THEN
    OUTPUT codes[foundIndex]
ELSE
    OUTPUT "No code"
END IF
```

3. Trace for `Cebu`:

| index | cities[index] | found | foundIndex |
| --- | --- | --- | --- |
| 0 | Manila | false | -1 |
| 1 | Cebu | true | 1 |

Output: `CEB`
