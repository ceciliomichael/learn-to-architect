# Module 09: Modules and Hierarchy Charts

## Before you start

Complete Modules 01 to 08. You should already know algorithms, pseudocode, sequence flowcharts, variables, constants, assignment, arithmetic expressions, and trace tables. You should be able to desk-check a short sequential design by hand.

## What you will learn

- why large problems are broken into modules
- what a module is in design work
- how a main module calls other modules
- how to write a simple module header
- how to draw a hierarchy chart as a tree of who calls whom
- how to keep each module focused on one job
- what parameters mean at a light conceptual level (data a module needs)

## Why this matters

A long list of steps becomes hard to read, hard to check, and hard to change. Modules let you name groups of related steps. A hierarchy chart shows the overall plan at a glance. When you later learn programming languages, functions and methods will feel familiar because you already practiced modular design.

## 1. One long list is hard to manage

Imagine a store checkout program written as one unbroken sequence:

```text
Display welcome message
Ask for item name
Ask for item price
Ask for quantity
Calculate line total
Ask whether tax applies
Calculate tax
Calculate grand total
Display receipt header
Display item details
Display tax
Display grand total
Display thank-you message
```

Each step may be correct. The problem is size. If the tax rule changes, you must hunt through the whole list. If you want to reuse the receipt display later, you copy a large block. If one part is wrong, the whole design feels tangled.

A better approach is to group related steps under clear names:

```text
Display welcome
Get purchase details
Calculate totals
Display receipt
```

Those names are modules. A **module** is a named group of steps that does one job.

## 2. What a module is

In this course, a module is a design unit, not a file and not a programming-language keyword yet. Think of it as a labeled box of instructions.

A good module:

- has a clear name that describes its job
- contains the steps needed for that job
- can be called from another module
- can be understood without reading the entire program

Examples of focused module names:

| Module name | Job |
| --- | --- |
| `GetStudentName` | Ask for and store a student name |
| `CalculateAverage` | Compute an average grade |
| `DisplayAttendanceReport` | Show attendance results |
| `ApplyDiscount` | Adjust a price using a discount rule |

Names often start with an action word: Get, Calculate, Display, Validate, Update.

## 3. The main module is the starting point

Every design needs a place where control begins. That place is the **main module**.

The main module usually:

1. starts the program
2. calls other modules in order
3. ends the program

It should not contain every detail. It should show the high-level plan.

### Example: grade summary program

```text
Module Main
    Call DisplayWelcome
    Call GetScores
    Call CalculateAverage
    Call DisplayResult
End Module
```

Reading Main alone tells you the story of the program. The details live in the called modules.

### What "call" means

When Main **calls** a module, control moves to that module. The called module runs its steps. When it finishes, control returns to the caller, usually at the next step after the call.

```text
Main starts
  -> DisplayWelcome runs, then returns
  -> GetScores runs, then returns
  -> CalculateAverage runs, then returns
  -> DisplayResult runs, then returns
Main ends
```

## 4. Module headers and module bodies

A **module header** names the module and, when needed, lists the data it expects. The **module body** contains the steps.

### Simple form without parameters

```text
Module DisplayWelcome
    Display "Welcome to the grade summary program."
End Module
```

### Form with parameters (data the module needs)

Sometimes a module needs values that were created elsewhere. Those values are **parameters**. A parameter is a named piece of data a module receives when it is called.

```text
Module DisplayResult(average)
    Display "Average grade: ", average
End Module
```

Here, `average` is a parameter. The module does not invent the average. It receives the average and displays it.

### Calling with data

```text
Module Main
    Declare Real average
    Call DisplayWelcome
    Call GetScores
    Call CalculateAverage() returning average
    Call DisplayResult(average)
End Module
```

Different textbooks write parameters in slightly different ways. What matters conceptually:

1. The caller provides the needed data.
2. The module uses that data for its job.
3. The module name plus its data needs should make sense on their own.

You will practice parameter details more later. For now, treat parameters as "inputs a module needs to do its work."

## 5. Keep each module focused on one job

A module should do one job that you can state in a short sentence.

### Focused design

```text
Module GetItemPrice
    Display "Enter item price: "
    Input price
End Module

Module CalculateTax(price)
    Set tax = price * 0.08
End Module

Module DisplayTotal(price, tax)
    Set total = price + tax
    Display "Total: ", total
End Module
```

Each module has one clear responsibility.

### Unfocused design

```text
Module DoEverything
    Display welcome
    Input price
    Calculate tax
    Display total
    Display thank you
    Update inventory count
    Send email receipt
End Module
```

`DoEverything` is hard to name, hard to test, and hard to reuse. If inventory rules change, you must edit a module that also handles greetings and taxes.

### A practical test

Ask:

1. Can I describe this module's job in one short sentence?
2. Would I ever want only part of this module by itself?
3. Does the name match every step inside?

If the answer to 2 is yes, or 3 is no, split the module.

## 6. Hierarchy charts show who calls whom

A **hierarchy chart** is a tree diagram that shows modules and call relationships. It does not show every detailed step. It shows structure.

Rules for hierarchy charts in this course:

- Put Main at the top.
- Put each called module under its caller.
- Draw lines from caller down to callee.
- A module that is called more than once can appear under each caller, or you can note reuse clearly. For beginners, showing each call path is fine.
- Do not put decision diamonds or loop arrows in a hierarchy chart. Those belong in flowcharts.

### Example: shopping receipt program

```text
                    Main
                      |
      ----------------+----------------
      |               |               |
DisplayWelcome   ProcessPurchase   DisplayThanks
                      |
           -----------+-----------
           |          |          |
      GetItemData  CalcTotals  ShowReceipt
```

What this chart tells you:

- Main calls three modules.
- ProcessPurchase calls three more modules.
- DisplayWelcome and DisplayThanks are top-level helpers under Main.

What this chart does not tell you:

- the exact formulas
- variable names inside each module
- whether a decision or loop exists inside a module

That detail lives in pseudocode and flowcharts for each module.

## 7. Build a hierarchy chart from a problem

### Problem

Design a classroom attendance helper:

1. Greet the teacher.
2. Ask for the class name.
3. Ask for total students.
4. Ask for present students.
5. Calculate absent students.
6. Calculate attendance percentage.
7. Display a short report.
8. Say goodbye.

### Step 1: Group the jobs

| Group | Job |
| --- | --- |
| Greeting | Welcome message |
| Input | Collect class data |
| Calculation | Absent count and percentage |
| Output | Report and goodbye |

A clean split might be:

- `DisplayWelcome`
- `GetAttendanceData`
- `CalculateAttendance`
- `DisplayReport`
- `DisplayGoodbye`

### Step 2: Draw the hierarchy chart

```text
                         Main
                           |
     ----------------------+----------------------
     |           |         |          |          |
DisplayWelcome  GetAttendanceData  CalculateAttendance  DisplayReport  DisplayGoodbye
```

### Step 3: Sketch Main

```text
Module Main
    Call DisplayWelcome
    Call GetAttendanceData
    Call CalculateAttendance
    Call DisplayReport
    Call DisplayGoodbye
End Module
```

### Step 4: Write one focused module body

```text
Module CalculateAttendance(totalStudents, presentStudents)
    Set absentStudents = totalStudents - presentStudents
    Set attendancePercent = (presentStudents / totalStudents) * 100
End Module
```

This module has one job: compute attendance values. It does not greet the teacher or print the report.

## 8. Modules, flowcharts, and hierarchy charts work together

These tools answer different questions:

| Tool | Question it answers |
| --- | --- |
| Hierarchy chart | Which modules exist, and who calls whom? |
| Pseudocode | What exact steps does each module perform? |
| Flowchart | How does control move step by step, including later decisions and loops? |
| Trace table | What values appear when you walk through the logic? |

A complete modular design often includes:

1. a hierarchy chart for the whole program
2. pseudocode for Main and each module
3. flowcharts for modules that need visual detail
4. trace tables for critical calculations

## 9. Sequence inside modules still matters

Modules do not replace sequence. Inside a module, steps still run in order unless a later lesson introduces decisions or loops.

```text
Module GetItemData
    Display "Enter item name: "
    Input itemName
    Display "Enter price: "
    Input price
    Display "Enter quantity: "
    Input quantity
End Module
```

If you swap the order of price and quantity prompts, the user experience changes. Modular design organizes the program. Sequence still controls the steps inside each box.

## 10. Light conceptual rules for data between modules

You already know variables store values. With modules, ask where a value is created and where it is needed.

### Example

```text
Module Main
    Declare String itemName
    Declare Real price
    Declare Integer quantity
    Declare Real lineTotal

    Call GetItemData(itemName, price, quantity)
    Call CalculateLineTotal(price, quantity, lineTotal)
    Call DisplayLine(itemName, lineTotal)
End Module
```

Conceptually:

- `GetItemData` needs a place to put the collected values.
- `CalculateLineTotal` needs price and quantity, and produces lineTotal.
- `DisplayLine` needs the name and the final amount.

You do not need formal programming syntax yet. You do need this habit:

1. Name the data.
2. Know which module creates it.
3. Know which module uses it.
4. Pass only what the module needs for its job.

Avoid giving every module access to every value "just in case." That hides the true dependencies.

## Predict the result

Read this design carefully.

```text
Module Main
    Call StepA
    Call StepB
    Call StepC
End Module

Module StepA
    Display "Open store"
End Module

Module StepB
    Display "Serve customer"
End Module

Module StepC
    Display "Close store"
End Module
```

1. What messages appear, and in what order?
2. Does Main display any message directly?
3. If you remove the call to `StepB`, what changes?

Write your answers before continuing.

Expected thinking:

1. Open store, then Serve customer, then Close store.
2. No. Main only calls modules.
3. Serve customer never appears. The other two messages still appear.

## Common mistakes

### Putting every step in Main

Main becomes a long list again. Split work into named modules and keep Main as the high-level plan.

### Naming modules after vague words

Names like `Process`, `DoStuff`, or `Module1` hide meaning. Prefer `CalculateTax` or `DisplayReceipt`.

### Mixing many jobs in one module

If a module both collects input and prints a full report, changes become risky. Split collection from display when both jobs are substantial.

### Drawing flowchart details inside a hierarchy chart

Hierarchy charts show call structure. Decisions, loops, and formulas belong in pseudocode and flowcharts.

### Forgetting that control returns after a call

After a called module ends, the caller continues with its next step. Designs fail when people assume the program ends inside a helper module.

### Passing no thought to needed data

If `DisplayResult` needs an average, the design must show where that average comes from. Parameters make that dependency visible.

## Check your understanding

1. What is a module in this course?
2. What is the role of the main module?
3. What does it mean to call a module?
4. What is a hierarchy chart used for?
5. Why should each module focus on one job?
6. In plain words, what is a parameter?

## Practice

1. Take a morning routine (wake up, get dressed, eat breakfast, leave home) and rewrite it as Main plus modules. Draw a hierarchy chart.
2. For a simple price program (get price, calculate 10 percent discount, display final price), write module headers and Main.
3. Improve this bad module name list: `Thing1`, `Process`, `Stuff`, `EndPart`. Replace each with a clear action name.
4. Draw a hierarchy chart for a program with Main calling `GetNames`, `SortNames`, and `PrintNames`, where `PrintNames` also calls `PrintHeader`.

Then complete the module exercises and quiz.

## Next step

Module 10 studies the three basic control structures: sequence, selection, and loop. You will also learn what spaghetti code is and how structured modular design keeps logic readable and maintainable.

Continue to [Module 10: Sequence, Selection, Loops, and Structured Design](../10-sequence-selection-loops-and-structured-design/README.md).
