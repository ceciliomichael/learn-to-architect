# Module 07 Exercise Solutions

## Warm-up solution

1. `5 + 4 * 2`  
   `4 * 2 = 8`, then `5 + 8 = 13`. Result: **13**

2. `(5 + 4) * 2`  
   `5 + 4 = 9`, then `9 * 2 = 18`. Result: **18**

3. `18 / 3 * 2`  
   Left to right: `18 / 3 = 6`, then `6 * 2 = 12`. Result: **12**

4. `18 / (3 * 2)`  
   `3 * 2 = 6`, then `18 / 6 = 3`. Result: **3**

5. `100 - 20 - 10`  
   Left to right: `100 - 20 = 80`, then `80 - 10 = 70`. Result: **70**

6. `100 - (20 - 10)`  
   `20 - 10 = 10`, then `100 - 10 = 90`. Result: **90**

## Guided exercise solution

### Pseudocode

```text
BEGIN
  DISPLAY "Enter score 1"
  INPUT score1
  DISPLAY "Enter score 2"
  INPUT score2
  DISPLAY "Enter score 3"
  INPUT score3
  SET sum = score1 + score2 + score3
  SET average = sum / 3
  DISPLAY average
END
```

One-expression alternative for the average line:

```text
SET average = (score1 + score2 + score3) / 3
```

Parentheses are required in that one-line form so addition happens before division. Without them, only the last score would be divided by 3.

### Desk check with 70, 85, 90

| Step | score1 | score2 | score3 | sum | average |
| --- | --- | --- | --- | --- | --- |
| after inputs | 70 | 85 | 90 |  |  |
| after sum | 70 | 85 | 90 | 245 |  |
| after average | 70 | 85 | 90 | 245 | 245 / 3 = 81.666... |

Displayed average: `81.666...` (exactly `245/3`).

### What goes wrong with the bad formula

```text
SET average = score1 + score2 + score3 / 3
```

Division happens before the full addition. For the sample:

- `score3 / 3 = 90 / 3 = 30`
- then `70 + 85 + 30 = 185`

That is not the average. The correct average is near 81.67, not 185.

## Independent exercise solution

### Pseudocode

```text
BEGIN
  CONSTANT DISCOUNT_RATE = 0.25
  CONSTANT TAX_RATE = 0.08
  DISPLAY "Enter original price"
  INPUT originalPrice
  SET discountAmount = originalPrice * DISCOUNT_RATE
  SET discountedPrice = originalPrice - discountAmount
  SET taxAmount = discountedPrice * TAX_RATE
  SET amountDue = discountedPrice + taxAmount
  DISPLAY amountDue
END
```

### Desk check with originalPrice `120`

| Name | Value |
| --- | --- |
| DISCOUNT_RATE | 0.25 |
| TAX_RATE | 0.08 |
| originalPrice | 120 |
| discountAmount | 120 * 0.25 = 30 |
| discountedPrice | 120 - 30 = 90 |
| taxAmount | 90 * 0.08 = 7.2 |
| amountDue | 90 + 7.2 = 97.2 |

Displayed amount due: `97.2`

### Valid alternative

```text
SET discountedPrice = originalPrice * (1 - DISCOUNT_RATE)
SET amountDue = discountedPrice * (1 + TAX_RATE)
```

With the sample:

- discounted price: `120 * 0.75 = 90`
- amount due: `90 * 1.08 = 97.2`

Same final result. The longer form with named intermediate amounts is often easier to check by hand.

## Debugging / desk-check task solution

### Problems

1. `temp1 + temp2 / 2` does not average two values. It divides only `temp2` by 2, then adds `temp1`.
2. The Fahrenheit line is less clear without parentheses, even though `* ` and `/` before `+` may already produce the usual conversion order. Clearer grouping is better.

### What the broken design computes for 10 and 20

```text
averageC = 10 + 20 / 2
         = 10 + 10
         = 20
averageF = 20 * 9 / 5 + 32
         = 180 / 5 + 32
         = 36 + 32
         = 68
```

Broken displayed value: `68`  
Intended Celsius average was `15`, not `20`.

### Corrected design

```text
BEGIN
  INPUT temp1
  INPUT temp2
  SET averageC = (temp1 + temp2) / 2
  SET averageF = (averageC * 9 / 5) + 32
  DISPLAY averageF
END
```

### Desk check of the corrected design

| Step | Value |
| --- | --- |
| temp1 | 10 |
| temp2 | 20 |
| averageC | (10 + 20) / 2 = 15 |
| averageF | (15 * 9 / 5) + 32 = 27 + 32 = 59 |

Displayed Fahrenheit value: `59`
