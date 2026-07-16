# Module 10: Sequence, Selection, Loops, and Structured Design

## Before you start

Complete Modules 01 to 09. You should be comfortable with algorithms, pseudocode, sequence flowcharts, variables, arithmetic, trace tables, modules, and hierarchy charts.

## What you will learn

- the three basic control structures: sequence, selection, and loop
- how to recognize each structure in small diagrams and pseudocode
- what spaghetti code is and why it causes trouble
- how to restructure messy jump-filled logic into structured modular design
- why structure improves readability and maintenance

## Why this matters

Almost every useful program is built from only a few control patterns. If you can see sequence, selection, and loop clearly, you can design new solutions and repair confusing ones. Structured design is the difference between logic you can trust and logic you are afraid to touch.

## 1. Three basic structures

A **control structure** is a pattern for deciding the order in which steps run.

The three basic structures are:

1. **Sequence**: steps run one after another.
2. **Selection**: the program chooses a path based on a condition.
3. **Loop**: the program repeats a path while a condition holds.

With modules, you can place these structures inside focused pieces of a larger design. The structures themselves stay simple.

## 2. Sequence

In a sequence, step A runs, then step B, then step C. There is no choice and no repetition.

### Plain-text flowchart

```text
[Start]
   |
   v
[Ask for price]
   |
   v
[Ask for quantity]
   |
   v
[Set total = price * quantity]
   |
   v
[Display total]
   |
   v
[End]
```

### Pseudocode

```text
Display "Enter price: "
Input price
Display "Enter quantity: "
Input quantity
Set total = price * quantity
Display "Total: ", total
```

You have used sequence since the early modules. It remains the default path inside any larger structure.

## 3. Selection

**Selection** means the program asks a true or false question, then chooses which steps to run.

You will study selection in depth in Modules 11 to 13. Here, learn to recognize it.

### Single choice idea

```text
If temperature is below 0 then
    Display "Freezing"
End If
```

If the condition is true, the display runs. If it is false, that display is skipped.

### Two-path idea

```text
If score >= 60 then
    Display "Pass"
Else
    Display "Needs review"
End If
```

Exactly one of the two messages appears.

### Plain-text decision shape

```text
          [score >= 60?]
           /         \
         Yes          No
          |            |
          v            v
   [Display Pass] [Display Needs review]
          \            /
           \          /
            v        v
           [next step]
```

The diamond-style decision is the classic flowchart mark for selection. Both paths should come back together before the next shared step when the structure is well formed.

## 4. Loop

A **loop** repeats one or more steps while a condition remains true, or until a stopping rule is met.

You will design loops in detail in Modules 14 to 16. Here, recognize the pattern.

### Example idea

```text
Set count = 1
While count <= 3
    Display "Practice round ", count
    Set count = count + 1
End While
```

### Plain-text loop shape

```text
[Set count = 1]
        |
        v
   [count <= 3?] --No--> [continue after loop]
        |
       Yes
        |
        v
[Display round]
        |
        v
[count = count + 1]
        |
        +---- back to test ----+
```

A healthy loop has:

1. a clear condition
2. steps that eventually make the condition fail (or otherwise stop the loop)
3. a single well-understood body of repeated work

## 5. Structured design combines the three cleanly

**Structured design** builds programs from sequence, selection, and loop, usually inside modules with one job each.

Key qualities of structured logic:

- each structure has one entry point
- each structure has one exit point
- paths do not jump wildly into the middle of other structures
- the reader can predict where control goes next

### Small structured example

```text
Module Main
    Call GetScore
    Call EvaluateScore
    Call DisplayMessage
End Module

Module EvaluateScore
    If score >= 90 then
        Set message = "Excellent"
    Else If score >= 60 then
        Set message = "Passing"
    Else
        Set message = "Keep practicing"
    End If
End Module
```

Main is sequence. EvaluateScore is selection. The overall design is modular and readable.

## 6. Spaghetti code

**Spaghetti code** is logic that is hard to follow because control jumps around with little clear structure. The name comes from tangled noodles: you cannot easily see where one strand begins and ends.

Common traits of spaghetti-style design:

- many jumps to distant labels
- paths that enter the middle of other sections
- repeated blocks copied with tiny differences
- decisions and loops that overlap in confusing ways
- no clear modules or hierarchy

### Unstructured jump-style sketch

Older designs sometimes used unrestricted jumps such as "go to step 4" or "go to label Retry" from many places.

```text
Step1: Input score
Step2: If score < 0 then GoTo Step1
Step3: If score > 100 then GoTo Bad
Step4: If score >= 60 then GoTo Pass
Step5: Display "Fail"
       GoTo EndLabel
Pass:  Display "Pass"
       GoTo EndLabel
Bad:   Display "Invalid"
       GoTo Step1
EndLabel: Display "Done"
```

This can be made to work for a tiny example. As soon as rules grow, the jumps multiply. Changing one label can break several paths. Desk-checking becomes painful because you must hunt for every GoTo.

## 7. Why spaghetti code is a problem

Spaghetti code causes practical damage:

1. **Hard to read.** A new reader cannot predict the next step.
2. **Hard to test.** You may miss rare jump paths.
3. **Hard to change.** A small rule change can require editing many distant lines.
4. **Hard to reuse.** Tangled sections do not become clean modules.
5. **Easy to break.** Fixing one bug can create another jump error.

Structured design does not remove complexity from the real world. It organizes complexity so humans can manage it.

## 8. Recognizing structure in a design

Use these questions:

### Sequence check

- Do these steps always run in the same order?
- Is there no decision and no repetition here?

### Selection check

- Is there a true or false condition?
- Does the design choose among alternate paths?
- Do the alternate paths rejoin cleanly afterward?

### Loop check

- Are some steps meant to happen more than once?
- Is there a condition that controls repetition?
- Is there a clear way for repetition to stop?

### Structure health check

- Can you circle one structure and see one way in and one way out?
- Does any path leap into the middle of another structure?
- Could this block become a well-named module?

## 9. Restructuring messy logic

### Messy version: temperature advice

```text
Input temperature
If temperature < 0 then GoTo Freezing
If temperature > 30 then GoTo Hot
Display "Mild day"
GoTo Finish
Freezing:
Display "Wear a coat"
GoTo Finish
Hot:
Display "Stay cool"
Finish:
Display "Have a good day"
```

### Problems

- Labels and jumps replace clear selection structure.
- The mild path is the "fall through" case, which is easy to miss while reading.
- Adding a new range would mean more labels and more GoTo lines.

### Structured rewrite

```text
Module Main
    Call GetTemperature
    Call ChooseAdvice
    Call DisplayClosing
End Module

Module GetTemperature
    Display "Enter temperature: "
    Input temperature
End Module

Module ChooseAdvice
    If temperature < 0 then
        Display "Wear a coat"
    Else If temperature > 30 then
        Display "Stay cool"
    Else
        Display "Mild day"
    End If
End Module

Module DisplayClosing
    Display "Have a good day"
End Module
```

### Hierarchy chart

```text
                 Main
                   |
     --------------+--------------
     |             |             |
GetTemperature ChooseAdvice DisplayClosing
```

### Why the rewrite is better

- Main shows the high-level sequence.
- Selection is visible as one IF/ELSE IF/ELSE block.
- No path jumps into the middle of another section.
- A future change, such as adding a rain warning module, has a clear place to land.

## 10. Nested structures stay structured when boundaries are clear

Structures can sit inside other structures. That is normal. The key is clean boundaries.

### Example: sequence inside selection

```text
If hasTicket is true then
    Display "Welcome"
    Display "Enjoy the event"
Else
    Display "Ticket required"
End If
```

### Example: selection inside a loop (preview idea)

```text
While moreStudents is true
    Input score
    If score >= 60 then
        Display "Pass"
    Else
        Display "Needs review"
    End If
    Input moreStudents
End While
```

Even with nesting, each structure should be readable as a unit: one entry, one exit, clear condition, clear body.

## 11. Structure helps maintenance

**Maintenance** means changing or repairing a design after it already exists.

Structured modular design helps because:

- You can find the right module quickly.
- You can change one structure without rewriting everything.
- You can desk-check one module with a small trace table.
- You can explain the design with a hierarchy chart plus short module notes.

### Maintenance scenario

A store currently gives this advice:

- total under 50: no free shipping
- total 50 or more: free shipping

Later, the rule becomes:

- total under 50: shipping 5
- total from 50 to 99.99: shipping 2
- total 100 or more: free shipping

In a structured selection module, you update one decision block. In spaghetti code, you may need to repair several jump targets and duplicated display lines.

## Predict the result

Identify the main structure in each fragment.

### Fragment A

```text
Set price = 12
Set quantity = 3
Set total = price * quantity
Display total
```

### Fragment B

```text
If attendancePercent >= 90 then
    Display "Excellent attendance"
Else
    Display "Attendance needs improvement"
End If
```

### Fragment C

```text
Set day = 1
While day <= 5
    Display "School day ", day
    Set day = day + 1
End While
```

Expected answers:

- A: sequence
- B: selection
- C: loop

## Common mistakes

### Calling any complicated design "selection"

Complexity alone does not define structure. Look for conditions, alternate paths, and repetition.

### Using jumps because they feel faster to write

A quick GoTo can create long-term cost. Prefer clear IF/ELSE and loop forms.

### Leaving paths that never rejoin

In selection, both branches should meet again at the next shared step when later work is shared. If each branch ends the whole program, make that intention obvious.

### Hiding a loop's stop condition

If you cannot explain when repetition ends, the loop is not ready.

### Building modules that still contain spaghetti inside

Modules help only if the steps inside them are structured too.

## Check your understanding

1. Name the three basic control structures.
2. What is spaghetti code?
3. What does it mean for a structure to have one entry and one exit?
4. Why are unrestricted jumps risky in large designs?
5. How do hierarchy charts and structured control flow work together?

## Practice

1. Label five short pseudocode fragments from daily life as sequence, selection, or loop.
2. Rewrite a jump-filled pass/fail sketch into structured IF/ELSE form.
3. Draw plain-text diagrams for one sequence, one selection, and one loop using a shopping or grades example.
4. Take one of your Module 09 modular designs and mark which modules are pure sequence today and which will need selection later.

Then complete the module exercises and quiz.

## Next step

Module 11 focuses on selection in detail: boolean true/false values, single-alternative and dual-alternative decisions, flowchart diamonds, and IF/ELSE/ENDIF pseudocode.

Continue to [Module 11: Selection Structures and Boolean Expressions](../11-selection-structures-and-boolean-expressions/README.md).
