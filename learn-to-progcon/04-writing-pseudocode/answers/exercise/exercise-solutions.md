# Module 04 Exercise Solutions

Your keyword synonyms can differ slightly (`DISPLAY` instead of `OUTPUT`, `BEGIN` instead of `START`) if the design stays consistent, precise, and easy to desk-check.

## Warm-up solution

```text
START
  INPUT hoursWorked
  INPUT hourlyRate
  SET pay = hoursWorked * hourlyRate
  OUTPUT pay
END
```

Desk-check: hours `10`, rate `15`

- pay = 10 * 15 = 150
- expected output: `150`

## Guided exercise solution

### 1. Inputs and output

- Inputs: three item prices
- Output: the sum of those prices

### 2-4. Pseudocode

```text
START
  INPUT price1
  INPUT price2
  INPUT price3
  SET sum = price1 + price2 + price3
  OUTPUT sum
END
```

### 5. Desk-check

prices `5`, `10`, `2.5`

- sum = 5 + 10 + 2.5 = 17.5
- expected output: `17.5`

## Independent exercise solution

### 1. Problem A

```text
START
  INPUT width
  INPUT height
  SET area = width * height
  OUTPUT area
END
```

### 2. Problem B

```text
START
  INPUT score1
  INPUT score2
  SET average = (score1 + score2) / 2
  OUTPUT average
END
```

### 3. Desk-check A

width `4`, height `3`

- area = 12
- expected output: `12`

### 4. Desk-check B

scores `88` and `92`

- average = 180 / 2 = 90
- expected output: `90`

### 5. Why this is pseudocode

These designs use structured plain keywords for people to read and check by hand. They are not written in a full programming language with strict runnable syntax and a required compiler or interpreter for this course stage.

## Debugging / desk-check task solution

### 1. Problems

Valid issues include:

1. Keywords are inconsistent and incomplete (`begin` lowercase, `print it` instead of `OUTPUT`/`DISPLAY`).
2. Names `x` and `y` do not show price and quantity meaning.
3. `total = x times y somehow` is not precise course style for a calculation line.
4. There is no clear `END`.
5. Body lines are not indented in a consistent structured way.
6. "print it" does not name the value being shown.

### 2. Corrected pseudocode

```text
START
  INPUT price
  INPUT quantity
  SET total = price * quantity
  OUTPUT total
END
```

### 3. Desk-check

price `6`, quantity `7`

- total = 42
- expected output: `42`

### 4. Optional alternative

```text
BEGIN
  INPUT price
  INPUT quantity
  SET total = price * quantity
  DISPLAY total
END
```

Same logic and same expected output of `42` for inputs 6 and 7.
