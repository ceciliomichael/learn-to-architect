# Module 17 Exercise Solutions

Your wording may differ. The structure, indexes, and results should match.

## Warm-up solution

```text
SET colors = ["red", "yellow", "blue", "purple"]
FOR index FROM 0 TO 3 STEP 1
    OUTPUT colors[index]
END FOR
```

Expected output:

```text
red
yellow
blue
purple
```

The middle value was replaced, a fourth color was added, and the loop stop index became 3 for size 4.

## Guided exercise solution

```text
SET scores = [80, 90, 70, 85, 95]

FOR index FROM 0 TO 4 STEP 1
    OUTPUT scores[index]
END FOR

OUTPUT "First score:" scores[0]
OUTPUT "Last score:" scores[4]
```

Expected output:

```text
80
90
70
85
95
First score: 80
Last score: 95
```

Desk-check for index `2`: `scores[2]` is `70`.

## Independent exercise solution

```text
// Size is 7. Valid indexes are 0 through 6.
SET highs = [22, 24, 21, 19, 25, 27, 23]

OUTPUT "Day 0 high:" highs[0]
OUTPUT "Day 6 high:" highs[6]

SET highs[3] = 20

FOR index FROM 0 TO 6 STEP 1
    OUTPUT highs[index]
END FOR
```

Expected output:

```text
Day 0 high: 22
Day 6 high: 23
22
24
21
20
25
27
23
```

## Debugging / desk-check task solution

Problems in the original:

1. `FOR index FROM 0 TO 3` tries index `3`, but valid indexes are only `0`, `1`, and `2`.
2. The first price is `prices[0]`, not `prices[1]`.

Corrected design:

```text
SET prices = [10, 4, 7]
SET total = 0
FOR index FROM 0 TO 2 STEP 1
    SET total = total + prices[index]
END FOR
OUTPUT total
OUTPUT "First price is" prices[0]
```

Expected results:

```text
total = 21
First price is 10
```
