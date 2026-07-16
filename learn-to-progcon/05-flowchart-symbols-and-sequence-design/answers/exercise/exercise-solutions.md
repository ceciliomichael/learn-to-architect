# Module 05 Exercise Solutions

## Warm-up solution

1. `START` uses a **terminal** (oval). It marks the beginning.
2. `Enter temperature in Celsius` uses **input/output** (parallelogram). The solution gets a value from outside.
3. `fahrenheit = (celsius * 9 / 5) + 32` uses a **process** (rectangle). It is a calculation.
4. `Display fahrenheit` uses **input/output** (parallelogram). The solution shows a result.
5. `Is celsius below 0?` uses a **decision** (diamond). It asks a yes/no question.
6. `END` uses a **terminal** (oval). It marks the finish.

## Guided exercise solution

### Symbol list

| Step | Symbol |
| --- | --- |
| BEGIN / START | terminal |
| DISPLAY "Enter price of item 1" | input/output |
| INPUT price1 | input/output |
| DISPLAY "Enter price of item 2" | input/output |
| INPUT price2 | input/output |
| SET total = price1 + price2 | process |
| DISPLAY total | input/output |
| END | terminal |

### Flowchart

```text
  +--------+
  | START  |
  +---+----+
      |
      v
  /--------------------------------\
 /  Display "Enter price of item 1" \
 \----------------+----------------/
                  |
                  v
  /--------------------------------\
 /  Input price1                     \
 \----------------+----------------/
                  |
                  v
  /--------------------------------\
 /  Display "Enter price of item 2"  \
 \----------------+----------------/
                  |
                  v
  /--------------------------------\
 /  Input price2                     \
 \----------------+----------------/
                  |
                  v
  +--------------------------------+
  | total = price1 + price2        |
  +----------------+---------------+
                   |
                   v
  /--------------------------------\
 /  Display total                    \
 \----------------+----------------/
                  |
                  v
             +--------+
             |  END   |
             +--------+
```

### Desk check

- `price1 = 25`
- `price2 = 15`
- `total = 25 + 15 = 40`
- displayed value: `40`

If your chart order matches the pseudocode, the walk-through should produce the same result.

## Independent exercise solution

Names may vary. One clear solution:

### Pseudocode

```text
BEGIN
  DISPLAY "Enter attendance for meeting 1"
  INPUT attend1
  DISPLAY "Enter attendance for meeting 2"
  INPUT attend2
  DISPLAY "Enter attendance for meeting 3"
  INPUT attend3
  SET totalAttend = attend1 + attend2 + attend3
  DISPLAY totalAttend
END
```

### Flowchart

```text
START
  |
  v
Display "Enter attendance for meeting 1"   (input/output)
  |
  v
Input attend1                              (input/output)
  |
  v
Display "Enter attendance for meeting 2"   (input/output)
  |
  v
Input attend2                              (input/output)
  |
  v
Display "Enter attendance for meeting 3"   (input/output)
  |
  v
Input attend3                              (input/output)
  |
  v
totalAttend = attend1 + attend2 + attend3  (process)
  |
  v
Display totalAttend                        (input/output)
  |
  v
END
```

### Desk check

- `attend1 = 10`, `attend2 = 12`, `attend3 = 9`
- `totalAttend = 10 + 12 + 9 = 31`
- displayed total: `31`

A valid alternative is to use names such as `m1`, `m2`, and `m3`, as long as the same names appear in both pseudocode and the flowchart.

## Debugging / desk-check task solution

### Problems in the broken design

1. Calculation runs before `hours` and `rate` are entered.
2. The pay calculation uses a parallelogram, but it should be a process rectangle.
3. The input steps use rectangles, but they should be input/output parallelograms.
4. There is no `END` terminal.

### Corrected order and symbols

1. START (terminal)
2. Enter hours (input/output)
3. Enter rate (input/output)
4. pay = hours * rate (process)
5. Display pay (input/output)
6. END (terminal)

### Corrected flowchart

```text
  +--------+
  | START  |
  +---+----+
      |
      v
  /------------------\
 /  Enter hours       \
 \---------+----------/
           |
           v
  /------------------\
 /  Enter rate        \
 \---------+----------/
           |
           v
  +------------------+
  | pay = hours * rate|
  +---------+--------+
            |
            v
  /------------------\
 /  Display pay       \
 \---------+----------/
           |
           v
      +--------+
      |  END   |
      +--------+
```

### Desk check

- `hours = 8`
- `rate = 15`
- `pay = 8 * 15 = 120`
- displayed pay: `120`

Reasoning: inputs must exist before the formula uses them. Shapes should signal the kind of step, not only hold text.
