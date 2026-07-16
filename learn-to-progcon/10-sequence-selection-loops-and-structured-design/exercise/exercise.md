# Module 10 Exercises

## Warm-up: Label the structure

For each fragment, write **sequence**, **selection**, or **loop**. Then explain your choice in one sentence.

### Fragment 1

```text
Display "Enter name: "
Input studentName
Display "Hello, ", studentName
```

### Fragment 2

```text
If temperature >= 30 then
    Display "Hot day"
End If
```

### Fragment 3

```text
Set bottles = 5
While bottles > 0
    Display "Bottles left: ", bottles
    Set bottles = bottles - 1
End While
```

### Fragment 4

```text
If total >= 50 then
    Display "Free shipping"
Else
    Display "Shipping is 5"
End If
```

### Fragment 5

```text
Set subtotal = price * quantity
Set tax = subtotal * 0.08
Set grandTotal = subtotal + tax
```

## Guided exercise: Recognize and redraw

Here is a messy jump-style design for a quiz score message:

```text
Input score
If score < 0 then GoTo Invalid
If score > 100 then GoTo Invalid
If score >= 60 then GoTo PassMsg
Display "Not passing yet"
GoTo EndPart
PassMsg:
Display "Passing score"
GoTo EndPart
Invalid:
Display "Score must be from 0 to 100"
EndPart:
Display "Check complete"
```

### Requirements

1. List at least three problems with this design style.
2. Rewrite it as structured pseudocode using selection only (no GoTo).
3. Draw a plain-text flowchart of your structured version.
4. Optionally place the logic in a small modular design with Main and one or two helpers.

## Independent exercise: Attendance door policy

A school event has this door policy:

1. Ask for the visitor's age.
2. Ask whether the visitor has a ticket (yes/no).
3. If age is under 12, display "Child guest area only."
4. Otherwise, if the visitor has a ticket, display "Enter main hall."
5. Otherwise, display "Ticket required."
6. Always display "Enjoy the event day." at the end.

### Requirements

1. Identify where sequence appears and where selection appears.
2. Write structured modular pseudocode (Main plus modules).
3. Draw a hierarchy chart.
4. Draw a plain-text flowchart for the decision module only.
5. Explain in three to five sentences why this is easier to maintain than a label-and-jump version.

## Debugging and desk-check task

A student claims this design is structured. Review it carefully.

```text
Input temperature
If temperature < 0 then GoTo Coat
Display "No coat needed"
GoTo After
Coat:
Display "Wear a coat"
If temperature < -10 then GoTo Gloves
After:
Display "Done"
GoTo Finish
Gloves:
Display "Wear gloves too"
Finish:
```

### Your tasks

1. Mark every jump and explain how control can become hard to follow.
2. State whether this is spaghetti-style logic and why.
3. Rewrite the design with clear sequence and selection only.
4. Desk-check your rewrite with temperature values `-15`, `-5`, and `10`.
5. Record the expected messages for each value.

## Completion checklist

- [ ] I can name and recognize sequence, selection, and loop.
- [ ] I can explain spaghetti code in plain language.
- [ ] I can redraw jump-filled logic as structured design.
- [ ] I can combine modules with clear control structures.
- [ ] I can desk-check structured selection with sample values.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
