# Module 06: Variables, Constants, and Assignment

## Before you start

Complete Modules 01 to 05. You should be able to:

- write sequential pseudocode
- draw a simple sequence flowchart
- follow an algorithm step by step with sample values

You still do not need a programming language. This module is about design: how a plan stores, names, and updates values.

## What you will learn

- what named storage means in a design
- how variables and constants differ
- how assignment works (right side first, then store on the left)
- clear naming rules for design work
- conceptual data types: text, number, and yes/no
- the difference between introducing a name and using that name later
- design notation such as `SET total = 0`

## Why this matters

Almost every useful program remembers something: a price, a name, a running total, a temperature. If you cannot store and update values clearly, later steps have nothing reliable to work with. Good naming and careful assignment prevent confusion before any code is typed.

## 1. Named storage

A computer program works with values. A value is a piece of information, such as `42`, `"Ada"`, or `true`.

Named storage means you attach a name to a value so later steps can refer to it. The name is like a labeled box. The box holds the current value. The label lets you find the box again.

Example idea:

- name: `price`
- current value: `19.99`

Later instructions can say "use `price`" instead of rewriting `19.99` everywhere. If the price changes, you update the box once. Steps that use `price` will see the new value.

In design work, you invent names that match the problem: `studentName`, `score1`, `taxRate`, `isPresent`.

## 2. Variables

A variable is a named storage location whose value can change while the solution runs.

Examples:

- `score` starts at 0, then becomes 10 after a correct answer
- `total` grows as each item price is added
- `remainingSeats` drops as people check in

In pseudocode, a common pattern is:

```text
SET count = 0
SET count = count + 1
```

After the second line, `count` holds a new value. The name stays the same. The contents of the box change.

Use a variable when the design must update a value over time.

## 3. Constants

A constant is a named value that should not change while the solution runs.

Examples:

- `TAX_RATE = 0.08` for a fixed tax percentage in this problem
- `PASSING_SCORE = 60` for a course rule that stays fixed in the design
- `MAX_CAPACITY = 30` for a room limit that does not change during the run

In pseudocode you might write:

```text
CONSTANT TAX_RATE = 0.08
SET tax = price * TAX_RATE
```

Why use a constant name instead of the raw number everywhere?

- The meaning is clearer: `TAX_RATE` explains the number.
- If the fixed value must be updated in a later version of the design, you change one place.
- Readers can see which values are allowed to change and which are not.

Course rule of thumb: if the value is fixed for the whole run, prefer a constant name. If the value must update during the run, use a variable.

## 4. Assignment: right side, then left side

Assignment stores a value into a named location.

A common design form is:

```text
SET total = price + tax
```

Read it carefully:

1. Evaluate the right side first: compute `price + tax`.
2. Store that result into the name on the left: `total`.

The `=` sign in design language means "becomes" or "is given the value," not a claim that both sides were already equal in math class.

### Example

```text
SET price = 50
SET tax = 4
SET total = price + tax
```

After these lines:

- `price` is 50
- `tax` is 4
- `total` is 54

### Updating with the same name

```text
SET points = 10
SET points = points + 5
```

Right side uses the current value of `points` (10), adds 5, and produces 15. Then 15 is stored back into `points`.

This is normal and useful. It is how running totals work.

### Predict the result

```text
SET a = 3
SET b = 7
SET a = b
SET b = 1
```

What are `a` and `b` at the end?

Walk through:

1. `a` becomes 3
2. `b` becomes 7
3. `a` becomes the current value of `b`, so `a` is 7
4. `b` becomes 1

Final values: `a` is 7, `b` is 1.

Notice that changing `b` after step 3 does not change `a`. Assignment copies a value at that moment. It does not permanently glue two names together.

## 5. Naming rules for clear designs

Good names reduce mistakes.

Follow these practical rules:

1. **Prefer meaning over mystery.** Use `totalPrice` instead of `x`.
2. **No spaces in a name.** Use `studentName` or `student_name`, not `student name`.
3. **Be consistent.** If you start with `attend1`, do not switch to `attendanceOne` later without reason.
4. **Match the problem language.** For grades, names like `score`, `average`, and `letter` fit better than `thing1`.
5. **Do not reuse one name for two unrelated meanings.** If `total` is a money total, do not later store a headcount in the same name.
6. **Keep names short enough to write, long enough to understand.** `t` is usually too short. `theFinalComputedCustomerCheckoutTotalAmount` is usually too long for a small design.

Style note: some designers write constants in uppercase with underscores (`MAX_SCORE`). Some write variables in camel case (`maxScore`). Either style is fine in this course if you stay consistent inside one design.

## 6. Conceptual data types

A data type is a kind of value. At this stage, you only need three conceptual types.

### Text (string)

Text is a sequence of characters. Names, messages, and codes are text.

Examples:

- `"Maria"`
- `"Room B"`
- `"A+"`

In design notes you may write:

```text
SET studentName = "Maria"
DISPLAY studentName
```

### Number

Numbers are for counting and calculation.

Examples:

- `0`
- `42`
- `19.99`
- `-5`

```text
SET quantity = 3
SET unitPrice = 12.50
SET lineTotal = quantity * unitPrice
```

### Yes/no (boolean)

A yes/no value answers a true/false question. Common design words are `true`/`false` or `yes`/`no`.

Examples:

- `isPresent = true`
- `isPaid = false`
- `hasDiscount = true`

```text
SET isPresent = true
DISPLAY isPresent
```

### Why types matter even before coding

If `age` is a number, adding 1 makes sense. If `name` is text, adding 1 usually does not make sense. Keeping types straight prevents nonsense steps such as `total = "twelve" + 3` in a money problem.

You do not need language-specific type keywords yet. In design comments you can note the intended kind:

```text
// studentName is text
// score is number
// isPassing is yes/no
```

## 7. Declaring vs using

Declaring (or introducing) a name means you create the named storage and often give it a first value.

Using a name means a later step reads that value.

### Introduce, then use

```text
SET score1 = 80          // introduce and assign
SET score2 = 90          // introduce and assign
SET sum = score1 + score2 // use score1 and score2; introduce sum
DISPLAY sum              // use sum
```

### Using a name before it has a value is a design error

Broken idea:

```text
SET average = sum / count
SET sum = 100
SET count = 4
```

Here `sum` and `count` are used before they are set. A human following the steps does not know what to divide.

Correct order:

```text
SET sum = 100
SET count = 4
SET average = sum / count
```

### First assignment as setup

Many designs begin by setting starting values:

```text
SET total = 0
SET count = 0
```

That is intentional. A running total often starts at zero before items are added.

## 8. Design notation for assignment

This course uses simple pseudocode forms:

```text
SET name = value
SET name = expression
CONSTANT NAME = value
INPUT name
DISPLAY name
```

Examples with everyday data:

```text
BEGIN
  CONSTANT TAX_RATE = 0.10
  DISPLAY "Enter item price"
  INPUT price
  SET tax = price * TAX_RATE
  SET total = price + tax
  DISPLAY total
END
```

Flowchart view of the same idea:

- input parallelogram for `price`
- process rectangles for `tax = ...` and `total = ...`
- output parallelogram for `total`
- the constant can be written near the top as a note or as an early process-style setup line, depending on your chart style

What matters is that every named value has a clear origin and a clear use.

## 9. Variables in sequence designs

Here is a complete sequential design for a simple average of three grades.

```text
BEGIN
  DISPLAY "Enter score 1"
  INPUT score1
  DISPLAY "Enter score 2"
  INPUT score2
  DISPLAY "Enter score 3"
  INPUT score3
  SET sum = score1 + score2 + score3
  SET average = sum / 3
  DISPLAY average
END
```

Named storage used:

| Name | Role | Conceptual type |
| --- | --- | --- |
| `score1` | first grade | number |
| `score2` | second grade | number |
| `score3` | third grade | number |
| `sum` | total of grades | number |
| `average` | mean grade | number |

Predict the result when the inputs are 70, 80, and 90:

- `sum` becomes 240
- `average` becomes 80
- displayed result is 80

## 10. Constants and variables together

Problem: compute a discounted price with a fixed discount rate of 15 percent.

```text
BEGIN
  CONSTANT DISCOUNT_RATE = 0.15
  DISPLAY "Enter original price"
  INPUT originalPrice
  SET discountAmount = originalPrice * DISCOUNT_RATE
  SET finalPrice = originalPrice - discountAmount
  DISPLAY finalPrice
END
```

Why `DISCOUNT_RATE` is a constant: the rate is fixed for this problem. Why `originalPrice`, `discountAmount`, and `finalPrice` are variables: they depend on the input or on calculations from that input.

If the business later changes the rate to 20 percent, you update one constant definition instead of hunting through many raw numbers.

## 11. Assignment does not mean "link forever"

This idea is worth repeating with a shopping example.

```text
SET itemPrice = 20
SET total = itemPrice
SET itemPrice = 25
```

After line 2, `total` is 20. After line 3, `itemPrice` is 25, but `total` is still 20 unless you assign it again.

If you want `total` to follow the new price, write a new assignment:

```text
SET total = itemPrice
```

Designers who forget this often expect two names to stay synchronized automatically. Assignment copies a value at one moment in time.

## 12. Keeping names aligned across pseudocode and flowcharts

If the pseudocode says `SET total = price * quantity`, the matching flowchart process box should use the same names. Do not invent `t = p * q` in the chart unless you also change the pseudocode. Mixed names make desk checking harder and create false bugs.

Checklist when you introduce a name:

1. Is the meaning clear from the name?
2. Is the first value set before the name is used in a calculation?
3. Is the conceptual type sensible for later operations?
4. Does every later reference use the same spelling?

## Common mistakes

1. **Using a name before assigning it**  
   Always set a value first, unless a later module teaches a safer pattern.

2. **Treating `=` as a math equality claim**  
   In design, `SET a = b` means "copy the value of `b` into `a`."

3. **Spaces or vague names**  
   `item price` is invalid as one name. `x` hides meaning.

4. **One name, two jobs**  
   Storing a student name in `total` and later storing a number in the same `total` confuses every reader.

5. **Hard-coding a fixed business value everywhere**  
   Prefer a constant name for rates, limits, and fixed thresholds used in the design.

6. **Forgetting that assignment copies values**  
   Updating one variable does not automatically update another.

7. **Mixing types without thinking**  
   A yes/no flag is not text. A price is not a name. Keep the kind of value consistent with the operations you perform.

## Check your understanding

1. What is the difference between a variable and a constant in a design?
2. In `SET total = price + tax`, which side is evaluated first?
3. Why is `studentName` clearer than `sn` for most learners?
4. Name the three conceptual data types from this module and give one example of each.
5. What is wrong with this order?

```text
SET bill = subtotal + tax
SET subtotal = 40
SET tax = 3
```

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

Module 07 covers arithmetic operations and expressions. You will write formulas for totals, averages, discounts, and tax with clear order of operations.
