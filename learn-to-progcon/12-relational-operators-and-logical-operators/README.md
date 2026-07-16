# Module 12: Relational Operators and Logical Operators

## Before you start

Complete Modules 01 to 11. You should understand boolean true/false values, single-alternative and dual-alternative selection, decision diamonds, and the difference between arithmetic and boolean expressions.

## What you will learn

- relational operators for comparing values
- how to write equal to and not equal to in pseudocode
- logical operators AND, OR, and NOT
- how to evaluate compound conditions
- precedence ideas when combining AND and OR
- why parentheses make complex conditions clearer

## Why this matters

Real decisions rarely use only one simple comparison. A shopper may need a coupon and a minimum total. A classroom tool may accept a score only if it is at least 0 and at most 100. Relational and logical operators let you write those rules precisely.

## 1. Relational operators compare values

A **relational operator** compares two values and produces true or false.

| Operator (symbol style) | Pseudocode words | Meaning | Example | Result when x = 7 |
| --- | --- | --- | --- | --- |
| `>` | GREATER THAN | greater than | `x > 5` | true |
| `<` | LESS THAN | less than | `x < 5` | false |
| `>=` | GREATER THAN OR EQUAL TO | at least | `x >= 7` | true |
| `<=` | LESS THAN OR EQUAL TO | at most | `x <= 6` | false |
| `==` | EQUAL TO | equal | `x == 7` | true |
| `!=` | NOT EQUAL TO | not equal | `x != 10` | true |

This course accepts either symbols or words in pseudocode, as long as you are consistent and clear.

Examples:

```text
If score >= 60 Then
    Display "Pass"
End If

If temperature < 0 Then
    Display "Freezing"
End If

If quantity == 0 Then
    Display "Out of stock"
End If

If name NOT EQUAL TO "Guest" Then
    Display "Welcome, registered user"
End If
```

## 2. Equality and inequality need care

### Equal to

```text
If day == "Saturday" Then
    Display "Weekend pricing"
End If
```

Both sides must represent the same value for the result to be true.

### Not equal to

```text
If status != "Paid" Then
    Display "Payment still due"
End If
```

### Common confusion with assignment

- Assignment stores a value: `Set score = 60`
- Equality tests a value: `score == 60`

In design work, write tests so a reader never confuses them.

## 3. Logical operators combine or reverse conditions

A **logical operator** works with boolean values.

| Operator | Meaning | Result is true when |
| --- | --- | --- |
| AND | both | both sides are true |
| OR | either | at least one side is true |
| NOT | reverse | the original value is false |

### AND

```text
If age >= 18 AND hasId == true Then
    Display "Entry allowed"
End If
```

| age >= 18 | hasId | Result |
| --- | --- | --- |
| true | true | true |
| true | false | false |
| false | true | false |
| false | false | false |

### OR

```text
If isWeekend == true OR isHoliday == true Then
    Display "No class today"
End If
```

| isWeekend | isHoliday | Result |
| --- | --- | --- |
| true | true | true |
| true | false | true |
| false | true | true |
| false | false | false |

### NOT

```text
If NOT isComplete Then
    Display "Work remains"
End If
```

| isComplete | NOT isComplete |
| --- | --- |
| true | false |
| false | true |

## 4. Evaluate compound conditions step by step

### Example: free shipping rule

Rule: free shipping when total is at least 50 and the shopper is a member.

```text
If total >= 50 AND isMember == true Then
    Set shipping = 0
Else
    Set shipping = 5
End If
```

Case study: total = 60, isMember = false

1. `total >= 50` -> true
2. `isMember == true` -> false
3. true AND false -> false
4. Else path runs, shipping = 5

### Example: classroom help session

Rule: invite a student if the score is below 60 or attendance is below 75.

```text
If score < 60 OR attendance < 75 Then
    Display "Please attend the help session"
End If
```

Case study: score = 82, attendance = 70

1. `score < 60` -> false
2. `attendance < 75` -> true
3. false OR true -> true
4. Display the invitation

## 5. Precedence when combining AND and OR

When AND and OR appear in the same condition, evaluation order matters.

A common and useful rule in many programming languages is:

1. evaluate relational comparisons first
2. evaluate NOT next
3. evaluate AND before OR
4. use parentheses to force the meaning you intend

Exact language rules can differ. In design work, do not rely on memory tricks alone. Use parentheses whenever a condition has more than one logical operator.

### Ambiguous style (avoid in your designs)

```text
If score >= 60 OR attendance >= 75 AND hasPermission == true Then
```

Readers may disagree about the intended grouping.

### Clear style with parentheses

Meaning A: permission is always required, and either score or attendance can qualify.

```text
If (score >= 60 OR attendance >= 75) AND hasPermission == true Then
    Display "Eligible"
End If
```

Meaning B: high score alone is enough, or attendance with permission is enough.

```text
If score >= 60 OR (attendance >= 75 AND hasPermission == true) Then
    Display "Eligible"
End If
```

These are different rules. Parentheses make the chosen rule obvious.

## 6. Practical parentheses patterns

### Both requirements must be true

```text
If (age >= 12) AND (hasTicket == true) Then
    Display "Enter main hall"
End If
```

### At least one qualifying reason

```text
If (day == "Saturday") OR (day == "Sunday") Then
    Display "Weekend"
End If
```

### A range style preview (deep practice in Module 13)

"Score is valid when it is at least 0 and at most 100."

```text
If (score >= 0) AND (score <= 100) Then
    Display "Score is in range"
Else
    Display "Score is invalid"
End If
```

Both comparisons are required. A single comparison cannot express a closed range safely.

### Reverse a whole condition

```text
If NOT ((quantity > 0) AND (price > 0)) Then
    Display "Order data is incomplete"
End If
```

## 7. Truth evaluation practice with familiar data

### Shopping checkout

```text
Set total = 42
Set hasCoupon = true
Set isMember = true

Set getsExtraDeal = (total >= 40 AND hasCoupon == true) OR isMember == true
```

Step by step:

1. `total >= 40` -> true
2. `hasCoupon == true` -> true
3. true AND true -> true
4. `isMember == true` -> true
5. true OR true -> true
6. `getsExtraDeal` is true

Even if membership were false, the first group would still make the whole expression true for these values.

### Attendance and grades

```text
Set score = 55
Set attendance = 92

If score >= 60 AND attendance >= 80 Then
    Display "Good standing"
Else
    Display "Review needed"
End If
```

Evaluation:

1. `score >= 60` -> false
2. `attendance >= 80` -> true
3. false AND true -> false
4. Else path: Review needed

AND is strict. One false side fails the whole AND expression.

## 8. Use boolean variables to simplify long conditions

Long conditions are easier when pieces have names.

```text
Set hasPassingScore = score >= 60
Set hasStrongAttendance = attendance >= 80
Set inGoodStanding = hasPassingScore AND hasStrongAttendance

If inGoodStanding Then
    Display "Good standing"
Else
    Display "Review needed"
End If
```

Benefits:

- each comparison can be checked alone
- the final IF reads like natural language
- desk checks can fill intermediate boolean columns

## 9. Selection designs with compound conditions

### Dual-alternative example

```text
If temperature < 0 OR windSpeed > 40 Then
    Display "Outdoor event delayed"
Else
    Display "Outdoor event is on"
End If
```

### Single-alternative example

```text
If NOT isRegistered Then
    Display "Please register before class"
End If
```

### Modular example

```text
Module DecideShipping(total, isMember, shipping)
    If total >= 50 AND isMember == true Then
        Set shipping = 0
    Else
        Set shipping = 5
    End If
End Module
```

The compound rule stays in one place, which makes maintenance easier.

## Predict the result

### Problem A

```text
Set age = 16
Set hasPermission = true
If age >= 18 OR hasPermission == true Then
    Display "May attend"
Else
    Display "May not attend"
End If
```

What is displayed?

### Problem B

```text
Set price = 25
Set quantity = 2
If price < 20 AND quantity >= 2 Then
    Display "Discount aisle"
Else
    Display "Standard aisle"
End If
```

What is displayed?

### Problem C

```text
Set isOpen = false
If NOT isOpen Then
    Display "Store closed"
End If
```

What is displayed?

Expected results:

- A: May attend, because OR needs only one true side and permission is true
- B: Standard aisle, because price < 20 is false, so AND is false
- C: Store closed, because NOT false is true

## Common mistakes

### Writing AND when the real rule is OR

"Weekend if Saturday or Sunday" needs OR. AND would require a day to be both Saturday and Sunday, which is impossible.

### Writing OR when both requirements are mandatory

"Adult with ID" needs AND. OR would allow entry with only one requirement.

### Forgetting parentheses in mixed AND/OR conditions

If both operators appear, write parentheses that match the real-world rule.

### Comparing ranges with one operator only

"Between 0 and 100 inclusive" needs two comparisons joined by AND.

### Using assignment style in a test

Use `==` or EQUAL TO for equality tests. Keep `Set x = value` for assignment.

### Assuming NOT applies to only one word without clear grouping

Prefer `NOT isComplete` or `NOT (score >= 60)` so the scope of NOT is obvious.

## Check your understanding

1. What does a relational operator produce?
2. When is an AND expression true?
3. When is an OR expression true?
4. What does NOT do to a boolean value?
5. Why should you use parentheses when AND and OR appear together?

## Practice

1. Write conditions for: temperature below 0, score at least 90, quantity not equal to 0.
2. Write an AND condition for free shipping: total at least 50 and member is true.
3. Write an OR condition for a closed school day: weekend or holiday.
4. Rewrite a mixed AND/OR eligibility rule with parentheses for two different meanings.
5. Desk-check one compound condition with three different data sets.

Then complete the module exercises and quiz.

## Next step

Module 13 studies range checks and nested decisions. You will design multi-branch logic carefully and keep decision order correct when several thresholds interact.

Continue to [Module 13: Range Checks and Nested Decisions](../13-range-checks-and-nested-decisions/README.md).
