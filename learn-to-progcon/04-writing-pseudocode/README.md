# Module 04: Writing Pseudocode

## Before you start

Complete Modules [01](../01-computers-programs-and-environments/README.md), [02](../02-problem-solving-and-the-program-development-cycle/README.md), and [03](../03-algorithms-and-precise-instructions/README.md).

You should already know:

- what a program is and how development cycles work
- what an algorithm is
- that good algorithms are ordered, precise, and finite

## What you will learn

By the end of this module, you will be able to:

- explain the purpose of pseudocode
- use common pseudocode keywords for sequence designs
- indent related lines to show structure
- choose readable names for values
- write a short sequential design that is not a full programming language

## Why this matters

Numbered plain steps are useful. Pseudocode adds a shared style so your designs are easier to read, share, and later translate into a language such as Python. It sits between casual notes and strict code.

## 1. What pseudocode is

**Pseudocode** is a way to write an algorithm using structured plain language and a small set of common keywords.

Properties of pseudocode:

- It is meant for people first.
- It follows a consistent style.
- It is precise enough to desk-check.
- It is **not** a full programming language with one official compiler.

There is no single worldwide law for pseudocode spelling. Courses and teams pick a house style. This course uses a clear style you will see again in later modules.

### Scope of this module

This lesson introduces only enough named-value and formula notation to read a straight sequence. You will use supplied formulas and familiar arithmetic, not invent complicated expressions. Module 06 explains variables, constants, and assignment carefully. Module 07 explains operators, precedence, division, units, and formula design. When a line below uses `SET` or a simple calculation, treat it as a first guided look rather than knowledge you were expected to bring into the module.

### Where pseudocode fits

```text
Problem
  -> Algorithm idea
    -> Pseudocode design
      -> Flowchart (Module 05) and later code (Python modules)
```

Pseudocode records the plan from Module 02 in a form that stays close to English while looking more like future code structure.

## 2. Purpose of pseudocode

People write pseudocode to:

1. **Clarify logic** before language syntax gets in the way
2. **Communicate** a method to classmates, teachers, or teammates
3. **Desk-check** with sample data
4. **Guide implementation** when a programming language is introduced later

Pseudocode does not replace testing of real programs. It helps you catch logic problems early. When you reach Python modules, you still run and test the code.

## 3. Common keywords in this course

You will use these keywords for sequential designs. Keywords are written in UPPERCASE so they stand out.

| Keyword | Meaning |
| --- | --- |
| `START` or `BEGIN` | Mark the beginning of the design |
| `END` | Mark the end of the design |
| `INPUT` | Read a value from the user or another source |
| `OUTPUT` or `DISPLAY` | Show a value or message |
| `SET` or `ASSIGN` | Store a value in a named place |
| `COMPUTE` | Calculate an expression and usually store it (often written with `SET`) |

This course treats `START`/`END` and `BEGIN`/`END` as equivalent. Pick one pair and stay consistent inside a design. Examples below use `START` and `END`.

`OUTPUT` and `DISPLAY` are also treated as equivalent. Examples mostly use `OUTPUT`.

### Minimal skeleton

```text
START
  // steps go here
END
```

Every complete design in this module should open with `START` (or `BEGIN`) and close with `END`. That makes the finite end of the algorithm visible.

## 4. INPUT and OUTPUT

### INPUT

`INPUT` brings a value into the design and gives it a name.

```text
INPUT price
INPUT quantity
INPUT studentName
```

After `INPUT price`, the name `price` holds the entered amount for later steps.

### OUTPUT / DISPLAY

`OUTPUT` shows a message or a value.

```text
OUTPUT total
OUTPUT "Thank you"
DISPLAY average
```

Text meant as a fixed message is written in quotation marks in these examples. Names without quotation marks refer to stored values.

### First full example: greet by name

```text
START
  INPUT userName
  OUTPUT "Hello"
  OUTPUT userName
END
```

If the input is `Sam`, a desk-check expects the messages `Hello` and `Sam` as two outputs. Combining text and a stored value is useful, but this module does not require a concatenation operator that has not been defined.

## 5. SET, ASSIGN, and COMPUTE

### SET / ASSIGN

`SET` stores a value in a name. `ASSIGN` means the same idea.

```text
SET taxRate = 0.08
SET count = 0
ASSIGN message = "Ready"
```

Think of the name on the left as a labeled box. The value on the right goes into that box.

### COMPUTE

`COMPUTE` highlights a calculation. Many designs simply use `SET` with an expression:

```text
COMPUTE taxAmount = price * taxRate
SET taxAmount = price * taxRate
```

Both lines mean: calculate `price * taxRate` and store the result as `taxAmount`. This course accepts either form. Prefer one form inside a single design.

### Example: total with tax

```text
START
  INPUT price
  SET taxRate = 0.08
  SET taxAmount = price * taxRate
  SET total = price + taxAmount
  OUTPUT total
END
```

Desk-check with `price = 50`:

- taxAmount = 4
- total = 54
- output `54`

## 6. Readable names

Names should help a reader know what a value means.

### Better names

- `price`
- `quantity`
- `subtotal`
- `taxAmount`
- `studentName`
- `quizScore1`

### Weaker names

- `x`
- `stuff`
- `n1`, `n2`, `n3` without context
- `thing`
- `data` for every value

Short names can be fine when the meaning is local and obvious (`sum`, `count`, `total`). If a name needs a long comment every time, rename it.

### Naming style in this course

- Use letters that form a clear word or short phrase.
- For multi-word ideas, `taxAmount` or `tax_amount` are both readable. Examples use `taxAmount` style.
- Do not reuse one name for two unrelated meanings in the same design.

## 7. Indentation for structure

**Indentation** means starting a line farther to the right to show that it belongs inside a larger block.

In sequential designs, indent all steps between `START` and `END`:

```text
START
  INPUT score1
  INPUT score2
  SET average = (score1 + score2) / 2
  OUTPUT average
END
```

Why indent?

- The eye sees the beginning and end clearly.
- Later, when selection and loops appear, indentation will show nested structure.
- Messy left-aligned walls of text hide mistakes.

Use a consistent indent, such as two or four spaces. Do not mix random spacing.

### Predict the structure

Which version is easier to scan?

Version A:

```text
START
INPUT a
INPUT b
SET total = a + b
OUTPUT total
END
```

Version B:

```text
START
  INPUT a
  INPUT b
  SET total = a + b
  OUTPUT total
END
```

Version B is the course style. Same logic, clearer structure.

## 8. Sequential designs

A **sequence** is a design where steps run one after another from top to bottom with no choices and no repeated blocks yet.

Most of this module practices pure sequence. Simple decisions may appear only when a problem requires them, written in plain IF form. Full selection design is taught later. For Module 04 exercises, prefer straight sequence unless the problem clearly needs a choice.

### Example: average of three scores

```text
START
  INPUT score1
  INPUT score2
  INPUT score3
  SET sum = score1 + score2 + score3
  SET average = sum / 3
  OUTPUT average
END
```

Desk-check: 70, 80, 90 -> sum 240 -> average 80.

### Example: muffin sale total

```text
START
  INPUT unitPrice
  INPUT quantity
  SET total = unitPrice * quantity
  OUTPUT total
END
```

Desk-check: unitPrice 2.5, quantity 4 -> total 10.

### Example: Celsius to Fahrenheit

```text
START
  INPUT celsius
  SET fahrenheit = (celsius * 9 / 5) + 32
  OUTPUT fahrenheit
END
```

Desk-check: celsius 0 -> fahrenheit 32.

### Example: tip amount and total

```text
START
  INPUT price
  INPUT tipPercent
  SET tipAmount = price * tipPercent / 100
  SET total = price + tipAmount
  OUTPUT tipAmount
  OUTPUT total
END
```

Desk-check: price 20, tipPercent 10 -> tipAmount 2, total 22.

## 9. Pseudocode is not a full programming language

Keep these differences clear.

| Pseudocode | Full programming language |
| --- | --- |
| Flexible wording within a house style | Strict syntax rules |
| No official compiler required | Must match language rules to run |
| Main goal is clear logic | Main goal includes executable behavior |
| Desk-check by hand | Run tests on a machine |

### What to avoid in ProgCon pseudocode

- Pretending that any English sentence is automatic pseudocode without structure
- Copying random language punctuation you do not understand yet
- Writing code in a real language and calling it pseudocode when the course asks for design form
- Skipping `START`/`END` and readable names

### Valid flexibility

These can all be acceptable if clear and consistent:

```text
SET total = price + taxAmount
COMPUTE total = price + taxAmount
ASSIGN total = price + taxAmount
```

```text
OUTPUT total
DISPLAY total
```

Pick a style and keep it steady inside one solution.

## 10. From algorithm list to pseudocode

Module 03 style:

```text
1. Input price.
2. Input quantity.
3. Set subtotal to price * quantity.
4. Output subtotal.
5. Stop.
```

Module 04 pseudocode style:

```text
START
  INPUT price
  INPUT quantity
  SET subtotal = price * quantity
  OUTPUT subtotal
END
```

Same algorithm. Clearer shared format.

### Worked conversion: bookstore line total before discount modules

Algorithm:

```text
1. Input bookPrice.
2. Input quantity.
3. Set total to bookPrice * quantity.
4. Output total.
5. Stop.
```

Pseudocode:

```text
START
  INPUT bookPrice
  INPUT quantity
  SET total = bookPrice * quantity
  OUTPUT total
END
```

## 11. Desk-checking pseudocode

To desk-check:

1. Write sample input values.
2. Move line by line from `START` toward `END`.
3. Update a small table of names and values.
4. Record what `OUTPUT` would show.
5. Compare with the expected result.

### Trace example

```text
START
  INPUT price
  SET taxRate = 0.05
  SET taxAmount = price * taxRate
  SET total = price + taxAmount
  OUTPUT total
END
```

Sample input: price = 40

| Step | price | taxRate | taxAmount | total | Output |
| --- | --- | --- | --- | --- | --- |
| after INPUT | 40 | | | | |
| after SET taxRate | 40 | 0.05 | | | |
| after SET taxAmount | 40 | 0.05 | 2 | | |
| after SET total | 40 | 0.05 | 2 | 42 | |
| after OUTPUT | 40 | 0.05 | 2 | 42 | 42 |

Expected result: `42`

Module 08 deepens trace tables. This light version is enough to verify sequential pseudocode now.

## 12. Putting keywords together: template

Use this template for many Module 04 problems:

```text
START
  INPUT firstValue
  INPUT secondValue
  SET result = // expression using the inputs
  OUTPUT result
END
```

Expand with more `INPUT`, `SET`, and `OUTPUT` lines as needed. Keep names meaningful. Keep indentation steady. End with `END`.

## Common mistakes

### Writing essays instead of steps

Long paragraphs hide order. Use short keyword lines.

### Forgetting START and END

Without them, the finite boundary of the design is less obvious.

### Using names that mean nothing

`SET x = y * z` forces readers to guess.

### Mixing several house styles in one design

Do not switch between `BEGIN` and `START`, or `OUTPUT` and random phrases, without reason.

### Treating pseudocode as if it already ran

Pseudocode still needs a hand-check. Keywords alone do not guarantee a correct formula.

### Treating the preview as prior knowledge

This module defines every pseudocode keyword it requires. Use only the supplied simple formulas. Variables and expression rules are taught in depth in Modules 06 and 07.

## Check your understanding

1. What is pseudocode, and what is it for?
2. What do `INPUT` and `OUTPUT` do?
3. What does `SET total = price * quantity` mean?
4. Why indent the lines between `START` and `END`?
5. Why is pseudocode not a full programming language?
6. Translate this algorithm line into course pseudocode: "Read the temperature and store it."

## Practice

Complete the [module exercises](./exercise/exercise.md). Then take the [module quiz](./quiz/quiz.md).

## Next step

In [Module 05](../05-flowchart-symbols-and-sequence-design/README.md), you will draw sequence flowcharts that match pseudocode using standard symbols and flow lines.
