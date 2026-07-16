# Module 19 Exercise Solutions

## Warm-up solution

```text
SET prices = [10, 4, 7, 9]
SET total = 0
FOR index FROM 0 TO 3 STEP 1
    SET total = total + prices[index]
END FOR
SET average = total / 4
OUTPUT total
OUTPUT average
```

Expected: total `30`, average `7.5`.

## Guided exercise solution

```text
SET scores = [88, 76, 95, 81, 90]
SET total = 0
SET maximum = scores[0]
SET minimum = scores[0]

FOR index FROM 0 TO 4 STEP 1
    OUTPUT scores[index]
    SET total = total + scores[index]
    IF scores[index] > maximum THEN
        SET maximum = scores[index]
    END IF
    IF scores[index] < minimum THEN
        SET minimum = scores[index]
    END IF
END FOR

SET average = total / 5
OUTPUT "Total:" total
OUTPUT "Average:" average
OUTPUT "Highest:" maximum
OUTPUT "Lowest:" minimum
```

Expected: total `430`, average `86`, highest `95`, lowest `76`.

Highest-score idea: start at 88, then 76 no change, 95 updates maximum, later values do not beat 95.

## Independent exercise solution

```text
SET temps = [18, 21, 19, 22, 0, 0, 0]
SET count = 4
SET total = 0

FOR index FROM 0 TO count - 1 STEP 1
    OUTPUT temps[index]
    SET total = total + temps[index]
END FOR

SET average = total / count
OUTPUT "Average:" average
```

Expected average: `20`.

Looping to index 6 would include the unused zeros and pull the average down incorrectly.

## Debugging / desk-check task solution

Problems:

1. Loop runs `index` to 3, but valid indexes are 0..2.
2. `maximum = 0` is accidental luck for these positive numbers, but the safe pattern still starts at `nums[0]`.

Corrected:

```text
SET nums = [5, 2, 9]
SET total = 0
SET maximum = nums[0]
FOR index FROM 0 TO 2 STEP 1
    SET total = total + nums[index]
    IF nums[index] > maximum THEN
        SET maximum = nums[index]
    END IF
END FOR
SET average = total / 3
OUTPUT total
OUTPUT average
OUTPUT maximum
```

Expected: total `16`, average about `5.333...`, maximum `9`.
