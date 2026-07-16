# Module 11 Exercises

## Warm-up: True or false

For each case, write the boolean result of the condition: **true** or **false**.

1. `score >= 60` when `score = 60`
2. `temperature < 0` when `temperature = 3`
3. `quantity == 0` when `quantity = 0`
4. `price > 100` when `price = 100`
5. `hasTicket` when `hasTicket = false`

Then label each expression below as **arithmetic** or **boolean**:

6. `price * quantity`
7. `average >= 90`
8. `(filled / total) * 100`
9. `name == "Lia"`

## Guided exercise: Freezing warning and pass message

### Part A: Single-alternative

Write pseudocode that:

1. Asks for a temperature.
2. If the temperature is below 0, displays "Freezing warning".
3. Always displays "Temperature check finished".

Also draw a plain-text flowchart.

### Part B: Dual-alternative

Write pseudocode that:

1. Asks for a quiz score.
2. If the score is at least 60, displays "Pass".
3. Otherwise displays "Needs review".

Provide a desk-check table for scores `72` and `45`.

## Independent exercise: Store coupon module design

A small store program must:

1. Display "Corner Mart Checkout".
2. Ask for item price.
3. Ask whether the shopper has a coupon (`true` or `false`).
4. If the shopper has a coupon, final price is price times 0.85.
5. Otherwise final price equals price.
6. Display the final price.
7. Display "Thank you for shopping."

### Requirements

1. Use modules with a hierarchy chart.
2. Put the selection inside a focused calculation or decision module.
3. Write full pseudocode for Main and every module.
4. Draw a plain-text decision flowchart for the discount choice.
5. Desk-check twice:
   - price `20`, hasCoupon `true`
   - price `20`, hasCoupon `false`

## Debugging and desk-check task

This design is incorrect or unclear in several ways:

```text
Input score
If score = 60
    Display "Pass"
Else
    Display "Needs review"
Display "Always shown?"
```

### Your tasks

1. List the problems. Think about assignment vs comparison, missing End If, and which lines belong to which path.
2. Rewrite the design as correct dual-alternative selection.
3. State whether "Always shown?" should run for every score, and place it correctly.
4. Desk-check your rewrite with scores `60`, `59`, and `95`.

## Completion checklist

- [ ] I can explain boolean true/false in plain language.
- [ ] I can write single-alternative and dual-alternative selection.
- [ ] I can draw a decision diamond flowchart in plain text.
- [ ] I can tell arithmetic expressions from boolean expressions.
- [ ] I can desk-check both the true path and the false path.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
