# Module 02: Problem Solving and the Program Development Cycle

## Before you start

Complete [Module 01](../01-computers-programs-and-environments/README.md).

You should already know:

- the input, processing, output, and storage model
- the difference between hardware and software
- what a program is
- the difference between source instructions and results

## What you will learn

By the end of this module, you will be able to:

- list the main steps of the program development cycle
- explain what happens in understand, plan, write, test, and maintain
- use IPO thinking (input, process, output) to frame a small problem
- describe why skipping steps causes rework
- apply the cycle to everyday problems such as grades, prices, and attendance

## Why this matters

Typing instructions too early is a common trap. People rush to "make something run" before they know what success looks like. Then they spend a long time fixing confusion that careful planning would have prevented. A simple cycle keeps your work ordered and saves effort.

## 1. Problem solving comes before typing

A **problem**, in this course, is a task that needs a clear result from given information.

Examples:

- Find the average of three quiz scores.
- Calculate a sale total with tax.
- Count how many students are present.
- Convert a temperature from Celsius to Fahrenheit.

**Problem solving** means finding a reliable method that turns the given information into the needed result. Writing a program is one way to record and reuse that method. The method must be clear first.

If you cannot explain the method to a careful person, you are not ready to trust a machine with it.

## 2. The program development cycle

The **program development cycle** is a repeatable set of steps for building a working program. Different books use slightly different names. This course uses five steps that cover the same work:

1. **Understand the problem**
2. **Plan the logic**
3. **Write the design or code**
4. **Test**
5. **Maintain and document**

The word **cycle** matters. After testing, you often return to an earlier step. After a user asks for a change, you understand the new need and plan again. Development is not a single straight line that never looks back.

```text
Understand --> Plan --> Write --> Test --> Maintain
    ^                                  |
    |                                  |
    +-------------- (repeat as needed) +
```

## 3. Step 1: Understand the problem

Before you invent steps, you must know what the problem is asking.

Ask:

1. What result do I need?
2. What information is given?
3. What information is missing?
4. Are there rules or limits?
5. What should happen in unusual cases?

### Example: shopping total

A shop says: "Calculate the total for one item with 8% tax."

Understanding notes:

- **Needed result**: total amount to pay
- **Given information**: item price, tax rate 8%
- **Missing information**: the actual price must be provided each time
- **Rules**: tax is 8% of the price; total is price plus tax
- **Unusual cases**: price should not be negative; non-number input is invalid (you can note this even before you design full error handling)

### Example: grade average

"Find the average of three quiz scores."

Understanding notes:

- **Needed result**: one average value
- **Given information**: three scores
- **Rules**: average = sum of scores divided by 3
- **Unusual cases**: scores outside 0 to 100 may need a policy later

### A short problem statement

Rewrite the problem in one or two plain sentences. If you cannot, you do not understand it yet.

Good:

```text
Read three quiz scores. Calculate and show their average.
```

Weak:

```text
Do grades.
```

"Do grades" does not say which grades, how many, or what result is required.

## 4. Step 2: Plan the logic

**Logic**, here, means the method: the order of actions and decisions that produce the result.

Planning can use:

- a numbered list of steps
- IPO notes (covered in section 8)
- later in the course: pseudocode and flowcharts

At this stage, focus on the method, not on language details.

### Plan for the tax total

```text
1. Get the item price.
2. Set tax rate to 0.08.
3. Compute tax amount = price * tax rate.
4. Compute total = price + tax amount.
5. Show the total.
```

### Plan for the grade average

```text
1. Get score1, score2, and score3.
2. Compute sum = score1 + score2 + score3.
3. Compute average = sum / 3.
4. Show the average.
```

A good plan is ordered. Someone else should be able to follow it with sample numbers and reach the same result.

### Predict the result

Using the tax plan, if the price is `50`, what total should appear?

Work by hand:

- tax amount = `50 * 0.08` = `4`
- total = `50 + 4` = `54`

Expected result: `54`

If your plan cannot support this hand check, the plan is not ready.

## 5. Step 3: Write the design or code

After the plan is clear, you record it in a form that can be followed carefully.

In early ProgCon modules, "write" often means:

- clean numbered steps
- pseudocode (Module 04)
- flowcharts (Module 05)

In later modules, "write" also means Python code that matches the design.

Writing is not the first step. Writing is where a good plan becomes a precise artifact.

### From rough plan to cleaner design

Rough note:

```text
get price, do tax, show stuff
```

Cleaner design:

```text
1. Input price.
2. Set taxRate to 0.08.
3. Compute taxAmount as price times taxRate.
4. Compute total as price plus taxAmount.
5. Output total.
```

The second version names values and states each action. That precision reduces mistakes.

## 6. Step 4: Test

**Testing** means checking that the method produces correct results for chosen examples.

You can test a design before any programming language exists. That is called **desk checking**: you act as the computer and follow the steps on paper with sample data. Later modules build full **trace tables**. For now, use simple hand checks.

### Test the average plan

Sample input: scores `70`, `80`, `90`

Hand check:

- sum = `70 + 80 + 90` = `240`
- average = `240 / 3` = `80`

Expected output: `80`

If the design said "divide by 2" by mistake, the hand check would show `120`, which fails a sensible expectation for three scores. Testing finds that error early.

### Choose useful test cases

Good beginner tests include:

- a normal case (typical numbers)
- a simple case (easy mental math)
- an edge case when relevant (price `0`, all scores equal)

You do not need dozens of tests for a tiny problem. You need honest checks that could reveal a wrong formula or a wrong order of steps.

### Testing is not optional decoration

A plan that has never been checked is only a hope. Checking turns hope into evidence.

## 7. Step 5: Maintain and document

**Maintenance** is the work of keeping a solution useful after it first works. Real programs change because:

- tax rates change
- a teacher wants four quiz scores instead of three
- a shop adds a discount rule
- a confusing message needs clearer wording

**Documentation** is clear writing that helps people understand the solution. It can include:

- a short problem statement
- assumptions (for example, tax rate is 8%)
- the design steps
- sample tests and expected results
- notes about known limits

Documentation does not need to be long. It needs to be accurate enough that future you (or a classmate) can update the solution without guessing.

### Small maintenance example

Original need: average of three scores.

New need: average of four scores.

Maintenance work:

1. Understand the new requirement.
2. Plan the new sum and divisor.
3. Update the design or code.
4. Test with four sample scores.
5. Update the notes that said "three scores."

Skipping the note update causes the next person to trust outdated instructions.

## 8. IPO thinking: input, process, output

**IPO** stands for Input, Process, Output. It is a compact way to understand and plan a problem.

| IPO part | Question |
| --- | --- |
| Input | What data do we need to receive? |
| Process | What work do we do with that data? |
| Output | What result do we produce? |

Storage can sit beside IPO when data must be saved. Many short designs still start with IPO because it forces clarity.

### IPO chart: attendance count

**Problem:** Count how many students are marked present in a list of three marks (`P` or `A`).

| Input | Process | Output |
| --- | --- | --- |
| mark1, mark2, mark3 | Start count at 0. Add 1 for each `P`. | presentCount |

Detailed process:

```text
1. Input mark1, mark2, mark3.
2. Set presentCount to 0.
3. If mark1 is P, add 1 to presentCount.
4. If mark2 is P, add 1 to presentCount.
5. If mark3 is P, add 1 to presentCount.
6. Output presentCount.
```

(Selection details grow in later modules. The point here is IPO structure.)

### IPO chart: temperature conversion

**Problem:** Convert Celsius to Fahrenheit.

| Input | Process | Output |
| --- | --- | --- |
| celsius | fahrenheit = (celsius * 9/5) + 32 | fahrenheit |

Hand check: if celsius is `0`, fahrenheit should be `32`.

## 9. Why skipping steps causes rework

**Rework** is work you must repeat because an earlier step was skipped or rushed.

### Skip understanding

You build a tool that averages homework points, but the teacher wanted quiz points only. You rewrite almost everything.

### Skip planning

You write random steps, then discover the tax is applied in the wrong place. You patch lines without a clear method, and new mistakes appear.

### Skip writing a clear design

You keep the plan only in your head. A week later you cannot remember the rules. You rebuild from incomplete memory.

### Skip testing

You deliver a total calculator that fails when the price is `0` or when someone enters text. Users lose trust. Fixing under pressure costs more than an early hand check.

### Skip maintenance notes

You change the tax rate in one place but leave old notes saying 8%. The next edit uses the wrong rate again.

### Cost picture

```text
Early clarity  --->  less rework later
Rushed typing  --->  more confusion, more rework
```

The cycle is not bureaucracy. It is a way to spend effort in the cheapest place: at the start, on understanding and planning.

## 10. Walking a full cycle with one problem

**Problem:** A bakery sells muffins for a given price each. Calculate the total for a customer who buys several muffins. No tax.

### Understand

- Result needed: total cost
- Inputs: price per muffin, quantity
- Rule: total = price * quantity
- Note: quantity should be a whole number in real shops; for now assume valid numbers are provided

Problem statement:

```text
Read the muffin price and the quantity purchased. Show the total cost.
```

### Plan

```text
1. Input price.
2. Input quantity.
3. Compute total = price * quantity.
4. Output total.
```

### Write (clean design)

```text
START
  INPUT price
  INPUT quantity
  SET total = price * quantity
  OUTPUT total
END
```

(You will formalize this style in Module 04. Here it only records the plan clearly.)

### Test

| price | quantity | expected total |
| --- | --- | --- |
| 2.50 | 4 | 10.00 |
| 3.00 | 1 | 3.00 |
| 2.00 | 0 | 0.00 |

### Maintain and document

Document:

```text
Problem: total = price * quantity for muffin sales.
Assumes valid numeric inputs.
Sample test: 2.50 and 4 produce 10.00.
```

If the bakery later adds a bulk discount, return to understand and plan. Do not only patch one line without updating tests and notes.

## 11. Matching the cycle to IPO and the computer system model

Module 01 gave you input, processing, output, and storage. This module gives you a workflow for creating programs that use those parts.

| Development step | How it uses earlier ideas |
| --- | --- |
| Understand | Identify required outputs and available inputs |
| Plan | Design the processing steps |
| Write | Record instructions that implement the plan |
| Test | Compare actual results with expected results |
| Maintain | Update instructions, stored rules, and notes over time |

You are not learning five unrelated topics. You are learning how people create reliable instructions for computer systems.

## Common mistakes

### Starting in the middle

Opening an editor and typing before writing a problem statement is starting in the middle. Pause and understand first.

### Planning only the happy path and never checking it

A plan that works only in your imagination is incomplete. Run at least one numeric hand check.

### Treating testing as "click around until it feels fine"

Feelings are not evidence. Use expected results written down in advance.

### Confusing documentation with decoration

Notes are part of maintenance. Outdated notes become new bugs.

### Believing the cycle is only for huge projects

Small problems benefit too. A five-line total still needs a clear formula and a quick check.

## Check your understanding

1. Name the five steps of the program development cycle used in this lesson.
2. What questions help you understand a problem?
3. What is IPO thinking?
4. Give one example of rework caused by skipping testing.
5. Why is development called a cycle instead of a one-way list?
6. For "average of three scores," what are the inputs and the output?

## Practice

Complete the [module exercises](./exercise/exercise.md). Then take the [module quiz](./quiz/quiz.md).

## Next step

In [Module 03](../03-algorithms-and-precise-instructions/README.md), you will learn what an algorithm is and how to write ordered, precise, finite steps for a problem.
