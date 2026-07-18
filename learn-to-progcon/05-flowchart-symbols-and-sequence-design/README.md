# Module 05: Flowchart Symbols and Sequence Design

## Before you start

Complete Modules 01 to 04. You should be able to:

- name the main steps of the program development cycle
- write a short algorithm with ordered steps
- write sequential pseudocode with clear input, process, and output lines

You do not need a programming language for this module. You need paper, a pencil, or a plain text editor.

## What you will learn

- the standard flowchart symbols used for start, end, process, input, output, and decisions
- how flow lines and connectors show order
- how to draw a sequence flowchart that matches pseudocode
- how to redraw a flowchart cleanly on paper
- how to read a flowchart from top to bottom without guessing

## Why this matters

Pseudocode uses words. A flowchart uses shapes and arrows. Both describe the same plan. A flowchart helps you see the order of work at a glance. Later, when solutions branch or repeat, the picture becomes even more useful. First you must learn the symbols and master simple sequences.

## 1. What a flowchart is

A flowchart is a diagram of an algorithm. Each shape stands for a kind of action. Arrows show which action happens next.

A flowchart is a design tool. It does not run on a computer by itself. It helps people understand the plan before coding. It also helps you find missing steps and wrong order early.

A sequence flowchart is the simplest kind. In a sequence, each step happens once, in a fixed order, with no choices and no repeats yet. That matches the sequential pseudocode you wrote in Module 04.

## 2. Terminal: start and end

A terminal symbol marks the beginning or the end of a flowchart. It is drawn as an oval or a rounded rectangle.

Common labels:

- `START`
- `END`
- `STOP`

Rules:

- Every complete flowchart has one clear start.
- A simple sequence usually has one clear end.
- Do not put calculation work inside the start or end oval. Those ovals only mark boundaries.

Text diagram:

```text
  +--------+
  | START  |
  +--------+
       |
       v
     ...
       |
       v
  +--------+
  |  END   |
  +--------+
```

On paper, draw a rounded box, write `START` or `END` inside it, and connect it with arrows.

## 3. Process: work the computer (or person) does

A process symbol is a rectangle. It holds one action that transforms data or updates storage.

Examples of process steps:

- Calculate the total price.
- Convert Celsius to Fahrenheit.
- Add 1 to the attendance count.
- Set the average from sum divided by count.

Write a short action phrase inside the rectangle. Prefer verbs that name the work:

- good: `total = price + tax`
- good: `Compute average`
- weak: `Numbers` (too vague)
- weak: `Do stuff` (not precise)

Text diagram:

```text
  +---------------------------+
  | total = price + tax       |
  +---------------------------+
```

One process box should hold one clear unit of work. If a step has several unrelated actions, split them into separate rectangles so the order stays visible.

## 4. Input and output: the parallelogram

An input/output symbol is a parallelogram (a slanted rectangle). Use it when the solution gets data from outside or shows a result.

Input examples:

- Read the student's name.
- Enter the temperature in Celsius.
- Get the item price.

Output examples:

- Display the total.
- Print the average grade.
- Show the receipt message.

Many designs use the same parallelogram shape for both input and output. The wording inside makes the difference clear.

Text diagram:

```text
  /---------------------------\
 /  Enter item price           \
 \-----------------------------/

  /---------------------------\
 /  Display total due          \
 \-----------------------------/
```

In plain text you may also write:

```text
[INPUT] Enter item price
[OUTPUT] Display total due
```

When you redraw on paper, use the slanted parallelogram if you can. If a text-only editor is all you have, label the step as input or output so the meaning stays clear.

## 5. Decision: a light preview of the diamond

A decision symbol is a diamond. It asks a yes/no question and chooses a path.

Example questions:

- Is the score at least 60?
- Is the cart empty?
- Is temperature below freezing?

Text diagram:

```text
           +---------------+
           | score >= 60 ? |
           +-------+-------+
                   |
          +--------+--------+
          |                 |
         Yes               No
          |                 |
          v                 v
     (pass path)       (fail path)
```

You only need a light preview now. Sequence designs in this module stay on a single path. Full decision design comes in later modules. Still, learn the diamond shape so you can recognize it when you see one.

Do not put a long calculation inside a decision diamond. The diamond holds the question. The work that follows goes in process or output boxes on each branch.

## 6. Flow lines and connectors

A flow line is an arrow that points from one symbol to the next. It shows control flow: which step happens after which.

Rules for clear flow lines:

- Draw arrows in a consistent direction when you can, usually top to bottom.
- Avoid crossing arrows when a cleaner layout is possible.
- Every symbol (except the final end) should have a clear next step.
- In a pure sequence, each step has exactly one outgoing arrow.

A connector is a small circle used when a chart is large and an arrow would become messy. Connectors with the same letter or number link one part of the page to another.

Simple connector idea:

```text
  ... end of page 1 ...
         (A)

  ... start of page 2 ...
         (A)
         |
         v
      next step
```

For short sequence charts, you often do not need connectors. Prefer a single page and straight arrows first.

## 7. Symbol summary

| Symbol name | Shape | Purpose | Example label |
| --- | --- | --- | --- |
| Terminal | Oval | Start or end | `START`, `END` |
| Process | Rectangle | Calculation or update | `total = price * quantity` |
| Input/Output | Parallelogram | Get data or show data | `Enter price`, `Display total` |
| Decision | Diamond | Yes/no question (preview) | `price > 0 ?` |
| Flow line | Arrow | Order of steps | points to next symbol |
| Connector | Small circle | Link distant parts | `A`, `B`, `1` |

Memorize the purpose of each shape. The shape is a standard signal so other people can read your chart quickly.

## 8. From pseudocode to a sequence flowchart

Pseudocode and flowcharts should match. Same steps. Same order. Same meaning.

Sample problem: compute a simple shopping total.

Pseudocode:

```text
BEGIN
  DISPLAY "Enter item price"
  INPUT price
  DISPLAY "Enter quantity"
  INPUT quantity
  SET total = price * quantity
  DISPLAY total
END
```

Matching sequence flowchart in text form:

```text
  +--------+
  | START  |
  +---+----+
      |
      v
  /---------------------------\
 /  Display "Enter item price" \
 \--------------+--------------/
                |
                v
  /---------------------------\
 /  Input price                 \
 \--------------+--------------/
                |
                v
  /---------------------------\
 /  Display "Enter quantity"    \
 \--------------+--------------/
                |
                v
  /---------------------------\
 /  Input quantity              \
 \--------------+--------------/
                |
                v
  +---------------------------+
  | total = price * quantity  |
  +-------------+-------------+
                |
                v
  /---------------------------\
 /  Display total               \
 \--------------+--------------/
                |
                v
           +--------+
           |  END   |
           +--------+
```

Notice the mapping:

- `BEGIN` and `END` become terminal ovals.
- `DISPLAY` and `INPUT` become parallelograms.
- `SET total = ...` becomes a process rectangle.
- Order of arrows matches the order of pseudocode lines.

If your flowchart and pseudocode disagree, fix one of them until they tell the same story.

## 9. How to redraw a flowchart on paper

Follow a calm redrawing routine:

1. Read the full problem and the pseudocode first.
2. List the steps in order on scrap paper.
3. Leave space at the top for `START` and at the bottom for `END`.
4. Draw symbols large enough for short labels.
5. Write short labels before you draw every arrow.
6. Connect symbols top to bottom with clear arrows.
7. Walk the chart with your finger from start to end.
8. Compare the walk-through with the pseudocode line by line.

Spacing tips:

- Keep one vertical path for a sequence.
- Align centers of symbols when possible.
- Do not squeeze labels. If a label is long, shorten the wording, not the meaning.
- Erase and redraw a messy section instead of stacking patches.

A clean chart is easier to check. A messy chart hides missing arrows and wrong order.

## 10. Reading a flowchart without guessing

To read a flowchart:

1. Find `START`.
2. Follow the only outgoing arrow.
3. Read the label in each shape.
4. Do what the shape means (input, process, or output).
5. Continue until `END`.

Predict the result for this chart with sample data.

```text
START
  |
  v
Input score1
  |
  v
Input score2
  |
  v
sum = score1 + score2
  |
  v
average = sum / 2
  |
  v
Display average
  |
  v
END
```

If `score1` is 80 and `score2` is 90, what is displayed?

Work it through:

- `sum` becomes 170
- `average` becomes 85
- the output is 85

That walk-through is desk checking in simple form. Module 08 turns it into a full trace table.

## 11. Common sequence designs

### Design A: message only

```text
START -> Display welcome message -> END
```

Useful for testing that output works, but most real tasks also need input and calculation.

### Design B: input, compute, output

```text
START
  -> Input values
  -> Process values
  -> Display result
  -> END
```

This pattern appears in grade averages, price totals, temperature conversion, and attendance totals.

### Design C: several inputs, one result

```text
START
  -> Input item1
  -> Input item2
  -> Input item3
  -> total = item1 + item2 + item3
  -> Display total
  -> END
```

Keep each input as its own parallelogram when order matters and clarity helps. Combining too much into one box can hide mistakes.

## 12. What a flowchart can and cannot check

A flowchart can help you:

- see missing steps
- check order
- compare the plan with pseudocode
- explain a design to another person

A flowchart cannot by itself:

- prove the formula is mathematically correct for every case
- replace running tests after the design becomes code
- fix unclear problem requirements

Use the flowchart as one design tool among several. Still write precise steps. Still check with sample values. Still test after coding later in the course.

## Common mistakes

1. **Missing START or END**  
   Without terminals, a reader does not know where the plan begins or finishes.

2. **Using the wrong shape**  
   Calculations belong in rectangles. Prompts and results belong in parallelograms. Do not put `Display total` in a process box if you are following standard symbols.

3. **Vague labels**  
   `Do calculation` is weaker than `average = sum / count`. Say what happens.

4. **Arrows that do not match pseudocode order**  
   If pseudocode inputs price before quantity, the flowchart must do the same.

5. **Crossing or looping arrows in a sequence chart**  
   A pure sequence is a single path. If you need a loop or a decision, that is a later structure, not a tangled sequence.

6. **Overcrowding**  
   Tiny symbols and long sentences make errors easy to miss. Prefer short labels and open spacing.

7. **Treating the chart as decoration**  
   Draw it so you can follow it. If you cannot walk through it with sample data, it is not finished.

## Check your understanding

1. Which shape marks the start or end of a flowchart?
2. Which shape holds a calculation such as `total = price * quantity`?
3. Why do input and output often share the same symbol shape?
4. What should match between a sequence flowchart and its pseudocode?
5. Name one thing a flowchart helps check and one thing it cannot fully prove.

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

In [Module 06](../06-variables-constants-and-assignment/README.md), you will give names to stored values and write designs that set and update those names with care.
