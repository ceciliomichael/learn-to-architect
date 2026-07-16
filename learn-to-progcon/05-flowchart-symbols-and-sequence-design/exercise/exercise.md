# Module 05 Exercises

## Warm-up: Label the symbols

For each step below, name the flowchart symbol you would use (terminal, process, input/output, or decision):

1. `START`
2. `Enter temperature in Celsius`
3. `fahrenheit = (celsius * 9 / 5) + 32`
4. `Display fahrenheit`
5. `Is celsius below 0?` (preview only)
6. `END`

Write one short reason for each choice.

## Guided exercise: Match pseudocode to a flowchart

Use this pseudocode for a two-item shopping total:

```text
BEGIN
  DISPLAY "Enter price of item 1"
  INPUT price1
  DISPLAY "Enter price of item 2"
  INPUT price2
  SET total = price1 + price2
  DISPLAY total
END
```

1. List every step in order on paper or in a text file.
2. Beside each step, write the symbol name (terminal, process, or input/output).
3. Draw the full sequence flowchart top to bottom. Use ovals, parallelograms, and a rectangle. Connect them with arrows.
4. Walk through the chart with `price1 = 25` and `price2 = 15`. Write the value of `total` and what is displayed.
5. Compare your chart with the original pseudocode line by line. Fix any mismatch.

Expected result for the sample values: total is 40, and 40 is displayed.

## Independent exercise: Attendance total flowchart

Problem: A club records attendance for three meetings. Design a sequential solution that:

- asks for attendance count for meeting 1, meeting 2, and meeting 3
- computes the total attendance across the three meetings
- displays the total

Requirements:

1. Write clear sequential pseudocode with `BEGIN` and `END`.
2. Draw a matching sequence flowchart with correct symbols.
3. Use short, precise labels (for example, `Input attend1`, not only `Data`).
4. Keep a pure sequence. Do not add decision branches.
5. Desk-check with sample values `10`, `12`, and `9`. State the displayed total.

Your names for the three attendance values may differ (`attend1` / `a1` / `meeting1Count`), but they must stay consistent between pseudocode and flowchart.

## Debugging / desk-check task

A learner drew this chart for converting hours worked into a simple pay message. Find every design problem and rewrite a correct sequence flowchart.

Broken design notes:

```text
START
  |
  v
pay = hours * rate     (drawn as a parallelogram)
  |
  v
Enter hours            (drawn as a rectangle)
  |
  v
Enter rate             (drawn as a rectangle)
  |
  v
Display pay
  |
  v
(no END oval)
```

What is wrong:

- wrong order (calculation before inputs)
- wrong shapes for several steps
- missing end terminal

Rewrite:

1. corrected step order
2. correct symbol for each step
3. full text flowchart from START to END
4. a desk-check with `hours = 8` and `rate = 15`, stating the displayed pay

## Completion checklist

- [ ] I can name terminal, process, input/output, and decision symbols.
- [ ] I can draw a sequence flowchart that matches pseudocode order.
- [ ] My labels are short and precise.
- [ ] I can walk a chart with sample values.
- [ ] I fixed wrong order and wrong shapes in the debugging task.

Compare your work with the [exercise solutions](../answers/exercise/exercise-solutions.md) after attempting every task.
