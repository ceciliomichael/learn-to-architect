# Module 03: Algorithms and Precise Instructions

## Before you start

Complete [Module 01](../01-computers-programs-and-environments/README.md) and [Module 02](../02-problem-solving-and-the-program-development-cycle/README.md).

You should already know:

- what a program is at a high level
- the program development cycle
- IPO thinking (input, process, output)

## What you will learn

By the end of this module, you will be able to:

- define an algorithm in plain language
- recognize that good algorithms are ordered, precise, and finite
- judge everyday instructions as clear or vague
- turn a short word problem into numbered steps
- explain how algorithms connect to programs without requiring a programming language yet

## Why this matters

Computers follow instructions exactly. If the instructions are fuzzy, the result is unreliable. An algorithm is the careful method behind a program. When you can write a good algorithm, design tools and languages become much easier to learn.

## 1. What an algorithm is

An **algorithm** is a clear set of steps that solves a problem or completes a task.

Everyday life is full of algorithms, even when people do not use that word:

- a recipe for rice
- directions from home to school
- the steps to compute a bill total
- a checklist for closing a shop

In programming concepts, an algorithm is the method you invent during planning. A program is one way to write that method so a computer can carry it out.

```text
Problem
   |
   v
Algorithm (clear method)
   |
   v
Design form (pseudocode, flowchart) or program code
   |
   v
Results when the steps run with real data
```

You can have an algorithm before you choose a programming language. That is a major goal of this course.

## 2. Properties of a good algorithm

A useful algorithm for computing work should be:

1. **Ordered**: steps have a sequence. Doing them in the wrong order can break the result.
2. **Precise**: each step says exactly what to do. Vague words leave too much guessing.
3. **Finite**: the steps end. The method does not wander forever without a stopping point.

These three properties are the core checklist for this module.

### Ordered

To compute a total with tax:

```text
1. Get the price.
2. Compute tax from the price.
3. Add price and tax.
4. Show the total.
```

If you show the total before you compute it, the order is wrong. Order is part of correctness.

### Precise

Vague step:

```text
Deal with the price.
```

Precise step:

```text
Set taxAmount to price * 0.08.
```

"Deal with" does not say calculate, store, discount, or display. Precise language names the action and the values.

### Finite

A finite algorithm reaches an end after a limited amount of work for normal inputs.

Finite:

```text
1. Input three scores.
2. Average them.
3. Output the average.
4. Stop.
```

Not finite in practice as written:

```text
1. Input a score.
2. Add it to a running total.
3. Go back to step 1.
```

That version never says when to stop accepting scores. Later modules teach safe loops with clear stopping rules. For now, notice that "forever" without an end is not a finished algorithm.

## 3. Everyday algorithms you already know

### Example A: Making a simple sandwich

```text
1. Place one slice of bread on a plate.
2. Add the filling on top of that slice.
3. Place the second slice of bread on the filling.
4. Stop.
```

This is ordered, fairly precise, and finite. It could be more precise about which filling, but the structure is sound.

### Example B: Finding a class average on paper

```text
1. Write down each student score.
2. Add all scores to get a sum.
3. Count how many scores you added.
4. Divide the sum by that count to get the average.
5. Write the average at the bottom of the page.
6. Stop.
```

### Example C: Checking if a shopper gets free shipping

```text
1. Get the cart total.
2. If the cart total is at least 50, announce free shipping.
3. Otherwise, announce that shipping costs 5.
4. Stop.
```

You do not need programming syntax to see the method. You only need clear steps.

## 4. Good algorithms versus vague algorithms

Compare these pairs.

### Pair 1: Attendance count

Vague:

```text
Look at attendance and figure it out.
```

Problems:

- look at which list?
- figure out what result?
- what counts as present?

Better:

```text
1. Start presentCount at 0.
2. Read the first mark. If it is P, add 1 to presentCount.
3. Read the second mark. If it is P, add 1 to presentCount.
4. Read the third mark. If it is P, add 1 to presentCount.
5. Show presentCount.
6. Stop.
```

### Pair 2: Sale total

Vague:

```text
Do the sale the usual way.
```

Problems:

- usual for whom?
- is tax included?
- one item or many?

Better:

```text
1. Input itemPrice.
2. Input quantity.
3. Set subtotal to itemPrice * quantity.
4. Set taxAmount to subtotal * 0.08.
5. Set total to subtotal + taxAmount.
6. Output total.
7. Stop.
```

### Pair 3: Temperature advice

Vague:

```text
Check the temperature and say something.
```

Better:

```text
1. Input temperature.
2. If temperature is below 0, output "Freezing".
3. Otherwise, output "Not freezing".
4. Stop.
```

### Checklist for spotting vagueness

Ask of each step:

- Does it name the action (input, compute, compare, output)?
- Does it name the values involved?
- Could two careful people disagree about what to do next?
- Is it clear when the whole method ends?

If two careful people disagree, the step is not precise enough yet.

## 5. Algorithms are not the same as programs

Keep these terms separate:

| Term | Meaning |
| --- | --- |
| Problem | The task or question to solve |
| Algorithm | The method: ordered, precise, finite steps |
| Program | Instructions written so a computer can perform a method, usually in a programming language |
| Results | What appears when the instructions run with data |

An algorithm can be written in plain numbered steps. A program is a later form, often with strict language rules. In this course, you practice algorithms first so language details do not hide thinking errors.

## 6. Turning a word problem into numbered steps

Use this small routine (it matches the development cycle, focused on the algorithm):

1. Underline or list the required result.
2. List the inputs.
3. Write the process as numbered steps.
4. Add a clear stop.
5. Hand-check with sample values.

### Worked example: bookstore discount

**Word problem:**

```text
A bookstore charges the listed price for a book. If the customer buys 3 or more copies of the same book, reduce the total by 10%. Show the final amount to pay for one book title.
```

**Required result:** final amount to pay  
**Inputs:** book price, quantity  
**Rules:** if quantity is 3 or more, apply 10% off the total; otherwise charge full total

**Algorithm:**

```text
1. Input bookPrice.
2. Input quantity.
3. Set total to bookPrice * quantity.
4. If quantity is greater than or equal to 3, set total to total * 0.90.
5. Output total.
6. Stop.
```

**Hand-check A:** price `10`, quantity `2`

- total = 20
- quantity is not >= 3, so no discount
- output `20`

**Hand-check B:** price `10`, quantity `3`

- total = 30
- quantity >= 3, so total = 30 * 0.90 = 27
- output `27`

If either hand-check fails, fix the algorithm before thinking about code.

### Worked example: pass or fail message

**Word problem:**

```text
Read one exam score. If the score is 60 or higher, show Pass. Otherwise show Fail.
```

**Algorithm:**

```text
1. Input score.
2. If score is greater than or equal to 60, output "Pass".
3. Otherwise, output "Fail".
4. Stop.
```

**Hand-check:** score `60` should output `Pass`. score `59` should output `Fail`.

### Worked example: simple average

**Word problem:**

```text
Read three temperatures for the day: morning, afternoon, and night. Show the average temperature.
```

**Algorithm:**

```text
1. Input morningTemp.
2. Input afternoonTemp.
3. Input nightTemp.
4. Set sum to morningTemp + afternoonTemp + nightTemp.
5. Set average to sum / 3.
6. Output average.
7. Stop.
```

**Hand-check:** 10, 20, 30 -> sum 60 -> average 20.

## 7. Precision details that beginners often skip

### Name the values

Weak:

```text
Add them.
```

Stronger:

```text
Set sum to score1 + score2 + score3.
```

### Say where results go

Weak:

```text
Calculate the tax.
```

Stronger:

```text
Set taxAmount to price * 0.08.
```

### Put decisions in clear form

Weak:

```text
Handle high totals differently.
```

Stronger:

```text
If total is at least 100, set shipping to 0.
Otherwise, set shipping to 5.
```

### End the method

Include stop, end, or a final output step so the finite property is obvious.

## 8. Predict the result

Read this algorithm. Do not skip ahead.

```text
1. Set price to 20.
2. Set quantity to 3.
3. Set subtotal to price * quantity.
4. Set total to subtotal.
5. If quantity is greater than 2, set total to subtotal - 5.
6. Output total.
7. Stop.
```

What value is output?

Work it through:

- subtotal = 60
- quantity > 2 is true, so total = 60 - 5 = 55
- output `55`

If you got a different number, re-check each step in order. Algorithms reward slow, exact reading.

## 9. From algorithm quality to later design tools

Later modules give you formats for writing algorithms more formally:

- **Pseudocode**: text that looks structured, but is not a full language (Module 04)
- **Flowcharts**: diagrams of the flow of steps (Module 05)

Those tools do not replace the properties in this module. If a flowchart is ordered, precise, and finite, it can represent a good algorithm. If it is vague, the shape alone will not save it.

## 10. Common algorithm patterns (preview only)

You will study these in depth later. For now, recognize them as algorithm shapes:

1. **Sequence**: steps one after another (this module's main focus)
2. **Selection**: choose between paths with if/otherwise
3. **Loop**: repeat steps until a condition ends the repetition

A complete programming toolbox uses all three. Your first skill is writing a clean sequence with precise names and a clear end, plus simple decisions when a word problem needs them.

## Common mistakes

### Writing goals instead of steps

"Get the right total" is a goal. An algorithm must say how.

### Leaving order unclear

If step numbers are missing and the text jumps around, order errors hide easily.

### Using private shortcuts

"Do the usual tax thing" is not precise for other readers or for a computer later.

### Forgetting to stop

An open-ended "keep going" without a finish rule is not finite.

### Skipping the hand-check

An algorithm that has never been tested with sample numbers is still only a draft.

### Mixing in language syntax too early

You do not need perfect programming punctuation to write a good algorithm. You need clear actions and clear values.

## Check your understanding

1. What is an algorithm?
2. Name the three properties of a good algorithm used in this lesson.
3. Why is "Handle the grades" a weak algorithm step?
4. How is an algorithm different from a program?
5. What five mini-steps help turn a word problem into numbered algorithm steps?
6. In the bookstore example, why does quantity `2` at price `10` output `20` while quantity `3` outputs `27`?

## Practice

Complete the [module exercises](./exercise/exercise.md). Then take the [module quiz](./quiz/quiz.md).

## Next step

In [Module 04](../04-writing-pseudocode/README.md), you will write algorithms in pseudocode form using common keywords, indentation, and readable names.
