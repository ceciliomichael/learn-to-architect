# Module 08 Exercise Solutions

## Warm-up solution

Expected final value: `(4 + 6) * 2 = 20`.

| Step | a | b | total | doubleTotal | Output |
| --- | --- | --- | --- | --- | --- |
| INPUT a | 4 |  |  |  |  |
| INPUT b | 4 | 6 |  |  |  |
| SET total = a + b | 4 | 6 | 10 |  |  |
| SET doubleTotal = total * 2 | 4 | 6 | 10 | 20 |  |
| DISPLAY doubleTotal | 4 | 6 | 10 | 20 | 20 |

Final displayed value: `20`.  
Expected value: `20`. They match.

## Guided exercise solution

### Prediction for price 80

- discount = `80 * 0.10 = 8`
- finalPrice = `80 - 8 = 72`

### Full trace for price 80

| Step | price | discount | finalPrice | Output |
| --- | --- | --- | --- | --- |
| INPUT price | 80 |  |  |  |
| SET discount = price * RATE | 80 | 8 |  |  |
| SET finalPrice = price - discount | 80 | 8 | 72 |  |
| DISPLAY finalPrice | 80 | 8 | 72 | 72 |

- `discount` first appears after `SET discount = price * RATE`.
- `finalPrice` first appears after `SET finalPrice = price - discount`.

### Second sample: price 50

| Step | price | discount | finalPrice | Output |
| --- | --- | --- | --- | --- |
| INPUT price | 50 |  |  |  |
| SET discount | 50 | 5 |  |  |
| SET finalPrice | 50 | 5 | 45 |  |
| DISPLAY finalPrice | 50 | 5 | 45 | 45 |

### Why two samples help

A rate formula can look right once by luck or weak checking. A second price shows whether the rate still scales correctly (`10%` of 50 should be 5, not still 8). Multiple samples reduce the chance that a wrong operator or wrong rate slips through.

## Independent exercise solution

One valid design:

```text
BEGIN
  INPUT temp1
  INPUT temp2
  INPUT temp3
  SET sum = temp1 + temp2 + temp3
  SET average = sum / 3
  DISPLAY average
END
```

### Expected average first

Sample temperatures: `10`, `20`, `30`.  
Expected average: `(10 + 20 + 30) / 3 = 20`.

### Trace table

| Step | temp1 | temp2 | temp3 | sum | average | Output |
| --- | --- | --- | --- | --- | --- | --- |
| INPUT temp1 | 10 |  |  |  |  |  |
| INPUT temp2 | 10 | 20 |  |  |  |  |
| INPUT temp3 | 10 | 20 | 30 |  |  |  |
| SET sum = ... | 10 | 20 | 30 | 60 |  |  |
| SET average = ... | 10 | 20 | 30 | 60 | 20 |  |
| DISPLAY average | 10 | 20 | 30 | 60 | 20 | 20 |

Output matches the expected average: `20`.

The `sum` column helps trust the final average because if `sum` is wrong, `average` cannot be trusted. Seeing `60` before dividing by 3 confirms the addition before the division.

## Debugging / desk-check task solution

### Attempted trace of the broken design

| Step | hours | rate | pay | Output | Notes |
| --- | --- | --- | --- | --- | --- |
| SET pay = hours * rate | ? | ? | ? |  | hours and rate are not set yet |
| INPUT hours | 8 | ? | ? |  | pay was already computed too early |
| INPUT rate | 8 | 15 | ? |  | pay still not updated |
| DISPLAY pay | 8 | 15 | ? | ? | no valid pay value was stored after inputs |

The table breaks at the first assignment because the right side uses unset names. Even if someone invents values early, `pay` is never recomputed after the real inputs arrive.

### Design defect

Wrong order: calculation happens before inputs. There is also no later assignment that updates `pay` after `hours` and `rate` exist.

### Corrected design

```text
BEGIN
  INPUT hours
  INPUT rate
  SET pay = hours * rate
  DISPLAY pay
END
```

### Correct trace for hours 8, rate 15

| Step | hours | rate | pay | Output |
| --- | --- | --- | --- | --- |
| INPUT hours | 8 |  |  |  |
| INPUT rate | 8 | 15 |  |  |
| SET pay = hours * rate | 8 | 15 | 120 |  |
| DISPLAY pay | 8 | 15 | 120 | 120 |

Displayed pay: `120`.

### Extra sample

`hours = 0`, `rate = 15` should display `0`.

This sample is useful because it checks the boundary where no hours are worked. A correct formula still multiplies cleanly. An order bug or a hardcoded pay value would be more likely to fail or look suspicious.
