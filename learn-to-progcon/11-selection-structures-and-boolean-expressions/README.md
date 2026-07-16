# Module 11: Selection Structures and Boolean Expressions

## Before you start

Complete Modules 01 to 10. You should know sequence design, modules, hierarchy charts, and the idea that selection is one of the three basic control structures.

## What you will learn

- what a boolean value is (true or false)
- single-alternative selection (if then)
- dual-alternative selection (if then else)
- how decision diamonds work in flowcharts
- pseudocode forms IF, ELSE, and ENDIF
- the difference between an arithmetic expression and a boolean expression
- how to write and evaluate simple conditions

## Why this matters

Programs constantly choose. Should a student pass? Is a price high enough for free shipping? Is a temperature below freezing? Selection structures turn those questions into clear true or false checks and then choose the correct path.

## 1. Boolean values: true and false

A **boolean** value is one of two answers:

- `true`
- `false`

In plain language, think "yes" and "no," but programming designs usually use true and false.

Examples of statements that are true or false:

| Statement | Boolean result for sample data |
| --- | --- |
| score is at least 60, when score is 72 | true |
| temperature is below 0, when temperature is 5 | false |
| name is equal to "Ava", when name is "Ava" | true |
| quantity is greater than 10, when quantity is 3 | false |

A **condition** is an expression the design evaluates as true or false. Selection uses conditions to choose a path.

## 2. Arithmetic expressions vs boolean expressions

An **arithmetic expression** calculates a number.

Examples:

```text
price * quantity
totalStudents - presentStudents
(score1 + score2) / 2
```

A **boolean expression** produces true or false.

Examples:

```text
score >= 60
temperature < 0
quantity == 0
hasTicket is equal to true
```

Compare them side by side:

| Kind | Example | Result type |
| --- | --- | --- |
| Arithmetic | `8 * 3` | number `24` |
| Boolean | `8 > 3` | boolean `true` |
| Arithmetic | `100 - 40` | number `60` |
| Boolean | `100 == 40` | boolean `false` |

You can store either kind of result:

```text
Set total = price * quantity
Set isLargeOrder = quantity >= 10
```

`total` holds a number. `isLargeOrder` holds true or false.

## 3. Single-alternative selection (if then)

**Single-alternative selection** means: if the condition is true, run some steps. If the condition is false, skip those steps. There is no separate "else" path.

### Pseudocode

```text
If temperature < 0 Then
    Display "Warning: freezing temperature"
End If
```

Some courses write `ENDIF` as one word. This course accepts clear forms such as `End If` or `ENDIF` as long as you are consistent.

### Behavior table

| temperature | Condition `temperature < 0` | Action |
| --- | --- | --- |
| -4 | true | Display the warning |
| 0 | false | Skip the warning |
| 12 | false | Skip the warning |

### Plain-text flowchart

```text
[Start]
   |
   v
[Input temperature]
   |
   v
[temperature < 0?]
    |        \
   Yes        No
    |          \
    v           \
[Display warning] \
    |              \
    +-------+-------+
            |
            v
          [End]
```

Only the Yes path contains extra work. Both paths continue to the same next step after the structure.

### Everyday examples

```text
If attendancePercent < 75 Then
    Display "Attendance is below the school target"
End If
```

```text
If quantity == 0 Then
    Display "That item is out of stock"
End If
```

Use single-alternative selection when something should happen only in the special case, and nothing special is required otherwise.

## 4. Dual-alternative selection (if then else)

**Dual-alternative selection** means: if the condition is true, run one path. Otherwise, run a different path. Exactly one of the two paths runs.

### Pseudocode

```text
If score >= 60 Then
    Display "Pass"
Else
    Display "Needs review"
End If
```

### Behavior table

| score | Condition | Path taken | Message |
| --- | --- | --- | --- |
| 85 | true | Then path | Pass |
| 60 | true | Then path | Pass |
| 59 | false | Else path | Needs review |

### Plain-text flowchart

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

### When to use dual-alternative selection

Use it when both outcomes need their own action.

Examples:

```text
If hasTicket == true Then
    Display "You may enter"
Else
    Display "A ticket is required"
End If
```

```text
If total >= 50 Then
    Set shipping = 0
Else
    Set shipping = 5
End If
```

If only one outcome needs action, single-alternative is enough. If both outcomes need action, use dual-alternative.

## 5. The decision diamond

In flowcharts, a **decision diamond** holds the condition.

Standard idea:

- one arrow enters the diamond
- two arrows leave the diamond, usually labeled Yes/No or True/False
- each leaving path leads to the steps for that answer
- structured designs bring the paths back together when later work is shared

### Good pattern

```text
          <> condition <>
           /          \
         Yes           No
          |             |
       [work A]      [work B]
          \             /
           +---- next --+
```

### Poor pattern to avoid

Do not leave one path floating with no clear continuation. Do not jump from inside one branch into the middle of the other branch. Keep the selection structure tidy, as Module 10 required.

## 6. Pseudocode shape and indentation

Indent the steps that belong to each branch. Indentation is for human readers. It shows structure.

### Clear indentation

```text
If average >= 90 Then
    Display "Excellent"
    Display "Keep up the strong work"
Else
    Display "Solid effort"
    Display "Review any missed questions"
End If
Display "Report finished"
```

`Report finished` is outside the selection, so it always runs.

### Reading rule

1. Evaluate the condition.
2. If true, run only the Then steps.
3. If false, run only the Else steps when an Else exists.
4. Continue with the first step after `End If`.

## 7. Simple conditions in practice

A **simple condition** compares values or checks a boolean directly.

### Relational comparisons (preview; full operator study is Module 12)

```text
age > 17
price <= 20
quantity != 0
name == "Noah"
```

### Using a boolean variable directly

```text
Set isOpen = true

If isOpen Then
    Display "The shop is open"
Else
    Display "The shop is closed"
End If
```

Because `isOpen` is already true or false, it can be the condition.

### Naming boolean results

```text
Set canCheckout = quantity > 0
If canCheckout Then
    Display "Ready to checkout"
Else
    Display "Add at least one item"
End If
```

A clear boolean name makes the selection easier to read.

## 8. Selection inside modules

Selection often lives inside a focused module.

```text
Module Main
    Call GetScore
    Call DisplayPassMessage
End Module

Module GetScore
    Display "Enter score: "
    Input score
End Module

Module DisplayPassMessage
    If score >= 60 Then
        Display "Pass"
    Else
        Display "Needs review"
    End If
End Module
```

Hierarchy chart:

```text
              Main
               |
        -------+-------
        |             |
    GetScore   DisplayPassMessage
```

Main stays sequential. The decision sits where the decision work belongs.

## 9. Desk-check a selection with a trace table

### Design

```text
Input price
Input hasCoupon

If hasCoupon == true Then
    Set finalPrice = price * 0.90
Else
    Set finalPrice = price
End If

Display finalPrice
```

### Trace 1

| Step | price | hasCoupon | Condition | finalPrice | Output |
| --- | --- | --- | --- | --- | --- |
| Input | 40 | true |  |  |  |
| Decision | 40 | true | true |  |  |
| Then path | 40 | true |  | 36 |  |
| Display | 40 | true |  | 36 | 36 |

### Trace 2

| Step | price | hasCoupon | Condition | finalPrice | Output |
| --- | --- | --- | --- | --- | --- |
| Input | 40 | false |  |  |  |
| Decision | 40 | false | false |  |  |
| Else path | 40 | false |  | 40 |  |
| Display | 40 | false |  | 40 | 40 |

Desk-checking selection means you must test at least one true case and one false case.

## Predict the result

### Problem A

```text
Set temperature = 31
If temperature > 30 Then
    Display "Hot"
End If
Display "Check complete"
```

What is displayed?

### Problem B

```text
Set score = 55
If score >= 60 Then
    Display "Pass"
Else
    Display "Needs review"
End If
```

What is displayed?

### Problem C

```text
Set quantity = 4
Set total = quantity * 2
Set isBulk = quantity >= 10
If isBulk Then
    Display "Bulk order"
Else
    Display "Standard order"
End If
```

What are the values of `total` and `isBulk`, and what is displayed?

Expected results:

- A: Hot, then Check complete
- B: Needs review
- C: total is 8, isBulk is false, display Standard order

## Common mistakes

### Using assignment thinking instead of a true or false condition

A condition must evaluate to true or false. "Set score = 60" is assignment, not a boolean test. A test looks like `score == 60` or `score >= 60`.

### Forgetting the false path when both outcomes need work

If both sides need different actions, use Else. A single-alternative structure cannot express two required outcomes cleanly.

### Putting later shared steps inside only one branch

If a message should always appear, place it after `End If`, not only in the Then branch.

### Confusing arithmetic results with boolean results

`price * 0.08` is a number. `price > 100` is true or false. Do not treat them as the same kind of expression.

### Writing conditions that humans cannot state in one sentence

If you cannot read the condition aloud as a clear yes/no question, simplify it or name an intermediate boolean.

## Check your understanding

1. What two values can a boolean expression produce?
2. How does single-alternative selection differ from dual-alternative selection?
3. What is the role of a decision diamond in a flowchart?
4. What is the difference between an arithmetic expression and a boolean expression?
5. Why should you test both a true case and a false case when desk-checking selection?

## Practice

1. Write a single-alternative design that warns when attendance is below 80 percent.
2. Write a dual-alternative design that chooses free shipping or paid shipping using total purchase amount.
3. Convert one of those designs into a plain-text flowchart with a decision diamond.
4. Create a tiny module-based version of a pass/fail message program.
5. Build a trace table for both true and false paths of your shipping design.

Then complete the module exercises and quiz.

## Next step

Module 12 studies relational operators and logical operators in detail. You will compare values with greater than, less than, equal to, and not equal to, and you will combine conditions with AND, OR, and NOT.

Continue to [Module 12: Relational Operators and Logical Operators](../12-relational-operators-and-logical-operators/README.md).
