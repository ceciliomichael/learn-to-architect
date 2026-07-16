# Module 02 Exercise Solutions

Your wording can differ. The important part is a clear cycle, clear IPO, and honest tests.

## Warm-up solution

One valid rewrite:

```text
Read an item price and calculate the total with 8% tax. Show the total.
```

- **Inputs**: item price; tax rate may be fixed at 8% or also input
- **Output**: total with tax
- **Rule**: taxAmount = price * 0.08, total = price + taxAmount

Another valid rewrite focuses on discount:

```text
Read an original price and a discount percent. Show the discounted price.
```

Both are better than "Handle store prices" because they state inputs, process, and result.

## Guided exercise solution

### 1. Understand

Problem statement:

```text
Read two exam scores and show their average.
```

Unusual case note: scores outside 0 to 100 may need a rule later.

### 2. Plan

```text
1. Input score1.
2. Input score2.
3. Compute sum = score1 + score2.
4. Compute average = sum / 2.
5. Output average.
```

### 3. Write (clean design)

```text
INPUT score1
INPUT score2
SET sum = score1 + score2
SET average = sum / 2
OUTPUT average
```

### 4. Test

Sample A: `70` and `90`

- sum = 160
- average = 80
- expected output: `80`

Sample B: `100` and `100`

- sum = 200
- average = 100
- expected output: `100`

### 5. Maintain and document

```text
Problem: average of two exam scores.
Formula: average = (score1 + score2) / 2.
Sample test: 70 and 90 produce 80.
```

## Independent exercise solution

### 1. IPO chart

| Input | Process | Output |
| --- | --- | --- |
| price, tipPercent | tipAmount = price * (tipPercent / 100); total = price + tipAmount | tipAmount, total |

### 2. Numbered plan

```text
1. Input price.
2. Input tipPercent (example: 15 means 15%).
3. Compute tipAmount = price * tipPercent / 100.
4. Compute total = price + tipAmount.
5. Output tipAmount.
6. Output total.
```

### 3. Desk-check

price = `12.00`, tipPercent = `15`

- tipAmount = 12.00 * 15 / 100 = 1.80
- total = 12.00 + 1.80 = 13.80

Expected: tip `1.80`, total `13.80`

### 4. Rework from skipping understand

If the designer assumes the cashier types `0.15` but the cashier types `15`, the tip becomes enormous (`12 * 15 = 180`). The design must be rewritten and retested after the input meaning is clarified.

### 5. Rework from skipping testing

Without a hand check, a wrong formula such as forgetting to divide by 100 can ship to users. Fixing it after people overpay creates emergency repairs, lost trust, and repeated edits under pressure.

## Debugging / desk-check task solution

Problems in the learner notes:

- "do tax" is not understanding. It does not define inputs, rate, or required output.
- Skipping the plan leaves the method unreviewed.
- "show price * 1.08" jumps to writing without a full, testable method and forgets naming and input clearly.
- A forgotten test value is not real testing.
- "finished forever" ignores maintenance when rates or rules change.

Corrected mini cycle for 8% tax total:

```text
Understand:
  Read an item price. Calculate total with 8% tax. Show the total.
  Inputs: price. Fixed rate: 0.08. Output: total.

Plan:
  1. Input price.
  2. Set taxRate to 0.08.
  3. taxAmount = price * taxRate.
  4. total = price + taxAmount.
  5. Output total.

Write:
  INPUT price
  SET taxRate = 0.08
  SET taxAmount = price * taxRate
  SET total = price + taxAmount
  OUTPUT total

Test:
  price 50 -> tax 4 -> total 54
  price 0  -> total 0

Maintain and document:
  Problem: total with 8% tax.
  Formula: total = price * 1.08 (same as price + price * 0.08).
  Sample: 50 produces 54.
  If the tax rate changes, update taxRate, tests, and this note.
```
