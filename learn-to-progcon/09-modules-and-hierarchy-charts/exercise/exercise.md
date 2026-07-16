# Module 09 Exercises

## Warm-up: Name the modules

A bakery program currently has one long list of steps:

1. Display a welcome message.
2. Ask for pastry name.
3. Ask for unit price.
4. Ask for quantity.
5. Calculate the line total.
6. Display the line total.
7. Display a goodbye message.

Split this into a main module plus focused modules. Write:

- a short hierarchy chart in plain text
- the Main module as pseudocode that only calls other modules
- a one-sentence job description for each module

## Guided exercise: Attendance modules

Design a modular solution for this problem:

- Welcome the user.
- Ask for total seats in a room.
- Ask for seats currently filled.
- Calculate empty seats.
- Calculate percent full: `(filled / total) * 100`
- Display empty seats and percent full.
- Thank the user.

### Requirements

1. Draw a hierarchy chart with Main at the top.
2. Write pseudocode for Main.
3. Write full pseudocode for every module under Main.
4. At a light conceptual level, show which modules need which data. For example, a calculate module needs total and filled counts.
5. Keep each module to one clear job.

Use familiar variable names such as `totalSeats`, `filledSeats`, `emptySeats`, and `percentFull`.

## Independent exercise: School supply checkout

A school store sells one item per transaction for this exercise.

The program must:

1. Display the store name: "Campus Supply Desk"
2. Ask for student name
3. Ask for item name
4. Ask for item price
5. Ask for quantity
6. Calculate subtotal as price times quantity
7. Calculate tax as subtotal times 0.05
8. Calculate grand total as subtotal plus tax
9. Display a receipt with student name, item name, quantity, subtotal, tax, and grand total
10. Display "Have a great day."

### Requirements

1. Create at least these modules (you may add more if useful):
   - one welcome module
   - one input module (or more, if you prefer a cleaner split)
   - one calculation module
   - one receipt display module
   - one goodbye module
2. Draw the hierarchy chart.
3. Write Main and every module in pseudocode.
4. Show parameters where a module needs data created elsewhere.
5. Write one short paragraph explaining why your split is better than one long Main module.

## Debugging and desk-check task

A student wrote this design:

```text
Module Main
    Call DisplayWelcome
    Call DisplayTotal
    Call GetPrice
    Call CalculateTotal
End Module

Module DisplayWelcome
    Display "Welcome"
End Module

Module GetPrice
    Display "Enter price: "
    Input price
End Module

Module CalculateTotal
    Set total = price * 1.08
End Module

Module DisplayTotal
    Display "Total is ", total
End Module
```

### Your tasks

1. List the problems in call order and data use.
2. Rewrite Main so the call order makes sense.
3. Adjust module headers so data dependencies are visible (parameters are fine at a conceptual level).
4. Desk-check your corrected design with `price = 50`.
5. State the expected displayed total.

## Completion checklist

- [ ] I can explain what a module is and why modular design helps.
- [ ] I can write a Main module that calls helpers in a sensible order.
- [ ] I can draw a hierarchy chart as a tree of callers and callees.
- [ ] I can keep each module focused on one job.
- [ ] I can identify data a module needs and show it as parameters at a conceptual level.
- [ ] I can spot a broken call order and fix it.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
