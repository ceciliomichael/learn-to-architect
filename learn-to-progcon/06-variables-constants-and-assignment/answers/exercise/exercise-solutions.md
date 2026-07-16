# Module 06 Exercise Solutions

## Warm-up solution

1. Shopper first name: name such as `firstName` or `shopperName`. **Variable** (input that depends on the person). Type: **text**.
2. Fixed sales tax rate 0.08: name such as `TAX_RATE`. **Constant**. Type: **number**.
3. Running purchase total: name such as `total` or `runningTotal`. **Variable**. Type: **number**.
4. Present flag: name such as `isPresent`. **Variable** (may change per student or update after check-in). Type: **yes/no**.
5. Room capacity 25: name such as `MAX_CAPACITY` or `CAPACITY`. **Constant** for this event design. Type: **number**.

Other clear names are fine if the role and type match.

## Guided exercise solution

### Pseudocode

```text
BEGIN
  DISPLAY "Enter notebook price"
  INPUT notebookPrice
  DISPLAY "Enter pen price"
  INPUT penPrice
  SET total = notebookPrice + penPrice
  DISPLAY total
END
```

### Variables and types

| Name | Conceptual type | Role |
| --- | --- | --- |
| `notebookPrice` | number | first input price |
| `penPrice` | number | second input price |
| `total` | number | sum of the two prices |

### Introduce vs use

- `INPUT notebookPrice` introduces `notebookPrice` with an input value.
- `INPUT penPrice` introduces `penPrice`.
- `SET total = notebookPrice + penPrice` uses both prices and introduces `total`.
- `DISPLAY total` uses `total`.

### Desk check with 45 and 12

| Step | notebookPrice | penPrice | total |
| --- | --- | --- | --- |
| after input notebook | 45 | (empty) | (empty) |
| after input pen | 45 | 12 | (empty) |
| after assignment to total | 45 | 12 | 57 |
| display | 45 | 12 | 57 (shown) |

Displayed result: `57`.

### Matching flowchart (text)

```text
START
  |
  v
Display "Enter notebook price"
  |
  v
Input notebookPrice
  |
  v
Display "Enter pen price"
  |
  v
Input penPrice
  |
  v
total = notebookPrice + penPrice
  |
  v
Display total
  |
  v
END
```

## Independent exercise solution

One complete design:

```text
BEGIN
  DISPLAY "Enter temperature in Celsius"
  INPUT celsius
  SET fahrenheit = (celsius * 9 / 5) + 32
  DISPLAY fahrenheit
END
```

### Names and types

| Name | Conceptual type |
| --- | --- |
| `celsius` | number |
| `fahrenheit` | number |

### Desk check with Celsius `10`

- `celsius = 10`
- `fahrenheit = (10 * 9 / 5) + 32`
- `fahrenheit = (90 / 5) + 32`
- `fahrenheit = 18 + 32`
- `fahrenheit = 50`
- displayed result: `50`

### Valid alternative with a named constant

```text
BEGIN
  CONSTANT FREEZE_OFFSET = 32
  DISPLAY "Enter temperature in Celsius"
  INPUT celsius
  SET fahrenheit = (celsius * 9 / 5) + FREEZE_OFFSET
  DISPLAY fahrenheit
END
```

The constant version is optional. It can make the fixed offset easier to see. Either form is acceptable when the formula and order are correct.

## Debugging / desk-check task solution

### Bugs in the broken design

1. `total` is computed before `price` and `tax` exist.
2. `tax` is computed after `total`, so `total` never receives the real tax amount.
3. `price` is overwritten with the text `"cheap"`, which conflicts with numeric money calculations.
4. Even if order were fixed, `total` would still need to be assigned after `tax` is known.

### Corrected pseudocode

```text
BEGIN
  CONSTANT TAX_RATE = 0.1
  DISPLAY "Enter price"
  INPUT price
  SET tax = price * TAX_RATE
  SET total = price + tax
  DISPLAY total
END
```

### Desk check with price `50`

| Step | price | tax | total |
| --- | --- | --- | --- |
| after constant defined | (empty) | (empty) | (empty) |
| after input | 50 | (empty) | (empty) |
| after tax assignment | 50 | 5 | (empty) |
| after total assignment | 50 | 5 | 55 |
| display | 50 | 5 | 55 (shown) |

Expected display: `55`.

Reasoning: introduce fixed rates first or early, read inputs next, compute dependent values only after their inputs exist, and keep money values numeric.
