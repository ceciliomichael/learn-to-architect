# Module 12 Exercises

## Warm-up: Evaluate the comparisons

Given:

```text
score = 78
temperature = -2
quantity = 0
name = "Ava"
```

Write true or false for each:

1. `score >= 60`
2. `score > 78`
3. `temperature < 0`
4. `quantity == 0`
5. `quantity != 0`
6. `name == "Ava"`
7. `name != "Guest"`

## Guided exercise: AND, OR, and NOT

### Part A

A library borrowing rule:

- The visitor may borrow if `hasLibraryCard` is true AND `hasOverdueBook` is false.

Write the condition with AND and NOT. Then fill this truth-style table:

| hasLibraryCard | hasOverdueBook | May borrow? |
| --- | --- | --- |
| true | false |  |
| true | true |  |
| false | false |  |
| false | true |  |

### Part B

A shop display rule:

- Show "Weekend sale" if day is Saturday OR day is Sunday.

Write the condition and evaluate it for `day = "Friday"` and `day = "Sunday"`.

### Part C

Explain the difference between these two rules in plain sentences:

```text
Rule1: total >= 50 AND isMember == true
Rule2: total >= 50 OR isMember == true
```

Use sample data `total = 40`, `isMember = true` in your explanation.

## Independent exercise: Event entry design

Design a modular program for an event gate:

1. Ask for age.
2. Ask whether the visitor has a ticket (true/false).
3. Ask whether the visitor has a parent present (true/false).
4. Entry is allowed if:
   - age is at least 18 AND hasTicket is true
   - OR age is under 18 AND hasTicket is true AND hasParentPresent is true
5. Display "Enter" or "Entry denied".

### Requirements

1. Write the compound condition with parentheses that make the grouping obvious.
2. Build Main and modules in pseudocode.
3. Draw a hierarchy chart.
4. Desk-check all four cases below and state the message for each:

| Case | age | hasTicket | hasParentPresent |
| --- | --- | --- | --- |
| A | 20 | true | false |
| B | 20 | false | true |
| C | 15 | true | true |
| D | 15 | true | false |

5. Briefly explain why parentheses are needed in the entry rule.

## Debugging and desk-check task

A student wrote this condition for valid scores from 0 to 100 inclusive:

```text
If score >= 0 OR score <= 100 Then
    Display "Valid"
Else
    Display "Invalid"
End If
```

### Your tasks

1. Explain why this condition is wrong.
2. Give one example value that is actually invalid in real life but would be called valid by this condition.
3. Write the corrected condition with AND.
4. Desk-check the corrected condition with `-1`, `0`, `50`, `100`, and `101`.

## Completion checklist

- [ ] I can use relational operators to form true/false comparisons.
- [ ] I can evaluate AND, OR, and NOT correctly.
- [ ] I can write parentheses that match the intended rule.
- [ ] I can desk-check compound conditions with multiple data sets.
- [ ] I can repair a broken range-style condition.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
