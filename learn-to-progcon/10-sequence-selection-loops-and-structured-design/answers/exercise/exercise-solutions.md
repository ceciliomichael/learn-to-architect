# Module 10 Exercise Solutions

## Warm-up solution

### Fragment 1

**Sequence.** The three steps always run in order with no choice and no repetition.

### Fragment 2

**Selection.** A condition decides whether the display step runs.

### Fragment 3

**Loop.** The display and decrease steps repeat while bottles remain.

### Fragment 4

**Selection.** The design chooses one of two display paths.

### Fragment 5

**Sequence.** Three calculations run one after another.

## Guided exercise solution

### Problems with the jump style

1. Control jumps to labels, so the reader must scan the whole fragment to see paths.
2. Pass and invalid handling are separated from the decision point by jumps.
3. Adding a new score band would mean more labels and more GoTo lines.
4. The design is harder to place cleanly inside a focused module.

### Structured rewrite

```text
Module Main
    Call GetScore
    Call EvaluateScore
    Call DisplayClosing
End Module

Module GetScore
    Display "Enter score: "
    Input score
End Module

Module EvaluateScore
    If score < 0 OR score > 100 then
        Display "Score must be from 0 to 100"
    Else If score >= 60 then
        Display "Passing score"
    Else
        Display "Not passing yet"
    End If
End Module

Module DisplayClosing
    Display "Check complete"
End Module
```

If compound `OR` has not been practiced yet, an equivalent nested form is also fine:

```text
If score < 0 then
    Display "Score must be from 0 to 100"
Else If score > 100 then
    Display "Score must be from 0 to 100"
Else If score >= 60 then
    Display "Passing score"
Else
    Display "Not passing yet"
End If
```

### Plain-text flowchart for EvaluateScore

```text
            [score < 0 or score > 100?]
                 /            \
               Yes             No
                |               |
                v               v
      [Display invalid]   [score >= 60?]
                |            /        \
                |          Yes         No
                |           |           |
                |           v           v
                |   [Display Passing] [Display Not passing]
                \           |           /
                 \          |          /
                  \         v         /
                   \--> [return/next]
```

### Hierarchy chart

```text
                Main
                  |
      ------------+------------
      |           |           |
  GetScore  EvaluateScore  DisplayClosing
```

## Independent exercise solution

### Where structures appear

- Sequence: ask for age, ask for ticket, then later display the final shared message.
- Selection: choose among child area, main hall, and ticket required.
- The overall Main module is a sequence of calls.

### Hierarchy chart

```text
                      Main
                        |
        ----------------+----------------
        |               |               |
  GetVisitorData  DecideEntryMessage  DisplayClosing
```

### Modular pseudocode

```text
Module Main
    Declare Integer age
    Declare String hasTicket

    Call GetVisitorData(age, hasTicket)
    Call DecideEntryMessage(age, hasTicket)
    Call DisplayClosing
End Module

Module GetVisitorData(age, hasTicket)
    Display "Enter age: "
    Input age
    Display "Do you have a ticket (yes/no): "
    Input hasTicket
End Module

Module DecideEntryMessage(age, hasTicket)
    If age < 12 then
        Display "Child guest area only."
    Else If hasTicket is equal to "yes" then
        Display "Enter main hall."
    Else
        Display "Ticket required."
    End If
End Module

Module DisplayClosing
    Display "Enjoy the event day."
End Module
```

### Plain-text flowchart for DecideEntryMessage

```text
              [age < 12?]
               /       \
             Yes        No
              |          |
              v          v
 [Child guest area]  [has ticket yes?]
              |         /        \
              |       Yes         No
              |        |           |
              |        v           v
              | [Enter main hall] [Ticket required]
              \        |           /
               \       |          /
                \      v         /
                 --> [return to Main]
```

### Why this is easier to maintain

The decision lives in one module with a clear IF/ELSE IF/ELSE shape. Main stays a short sequence. If the child age cutoff changes, you edit one condition. If the closing message changes, you edit one display module. A jump-label version would scatter those rules across distant targets and make desk checks slower.

## Debugging and desk-check task solution

### Jump map and readability issues

1. `GoTo Coat` leaves the normal path for cold temperatures.
2. `GoTo After` skips the coat branch for mild temperatures.
3. From `Coat`, another jump to `Gloves` may skip `After` entirely depending on path.
4. `GoTo Finish` from `After` skips gloves handling, while the gloves path falls into Finish by position.
5. A reader must simulate every label to know whether "Done" appears, and in what order relative to clothing advice.

### Is it spaghetti-style?

Yes. The design relies on scattered labels and jumps. Paths enter different sections without a single clear selection structure. Small edits would be risky.

### Structured rewrite

```text
Display "Enter temperature: "
Input temperature

If temperature < 0 then
    Display "Wear a coat"
    If temperature < -10 then
        Display "Wear gloves too"
    End If
Else
    Display "No coat needed"
End If

Display "Done"
```

This uses sequence plus nested selection. No GoTo is required.

### Desk check

| temperature | Messages |
| --- | --- |
| -15 | Wear a coat / Wear gloves too / Done |
| -5 | Wear a coat / Done |
| 10 | No coat needed / Done |

Reasoning:

- `-15` is below 0 and also below -10, so both clothing messages appear, then Done.
- `-5` is below 0 but not below -10, so only the coat message appears, then Done.
- `10` takes the Else path, then Done.
