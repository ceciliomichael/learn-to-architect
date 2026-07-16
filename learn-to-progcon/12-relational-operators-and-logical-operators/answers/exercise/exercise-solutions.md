# Module 12 Exercise Solutions

## Warm-up solution

1. true
2. false
3. true
4. true
5. false
6. true
7. true

## Guided exercise solution

### Part A

Condition:

```text
hasLibraryCard == true AND NOT hasOverdueBook
```

Equivalent form:

```text
hasLibraryCard == true AND hasOverdueBook == false
```

Table:

| hasLibraryCard | hasOverdueBook | May borrow? |
| --- | --- | --- |
| true | false | true |
| true | true | false |
| false | false | false |
| false | true | false |

Reasoning: borrowing requires the card and also requires that the overdue flag is false.

### Part B

Condition:

```text
day == "Saturday" OR day == "Sunday"
```

Evaluations:

- `day = "Friday"` -> false OR false -> false (do not show weekend sale)
- `day = "Sunday"` -> false OR true -> true (show weekend sale)

### Part C

`Rule1` requires both a high enough total and membership. With total 40 and isMember true:

- `total >= 50` is false
- false AND true is false
- Rule1 fails

`Rule2` requires either a high enough total or membership. With the same data:

- false OR true is true
- Rule2 succeeds

So membership alone is enough for Rule2, but not for Rule1.

## Independent exercise solution

### Clear compound condition

```text
(age >= 18 AND hasTicket == true) OR (age < 18 AND hasTicket == true AND hasParentPresent == true)
```

A factored form is also acceptable if it keeps the meaning obvious:

```text
hasTicket == true AND (age >= 18 OR (age < 18 AND hasParentPresent == true))
```

Both forms require a ticket. Adults need only the ticket. Minors also need a parent present.

### Hierarchy chart

```text
                    Main
                      |
        --------------+--------------
        |             |             |
  GetVisitorData  DecideEntry   DisplayResult
```

### Pseudocode

```text
Module Main
    Declare Integer age
    Declare Boolean hasTicket
    Declare Boolean hasParentPresent
    Declare Boolean mayEnter

    Call GetVisitorData(age, hasTicket, hasParentPresent)
    Call DecideEntry(age, hasTicket, hasParentPresent, mayEnter)
    Call DisplayResult(mayEnter)
End Module

Module GetVisitorData(age, hasTicket, hasParentPresent)
    Display "Enter age: "
    Input age
    Display "Has ticket (true/false): "
    Input hasTicket
    Display "Parent present (true/false): "
    Input hasParentPresent
End Module

Module DecideEntry(age, hasTicket, hasParentPresent, mayEnter)
    If (age >= 18 AND hasTicket == true) OR (age < 18 AND hasTicket == true AND hasParentPresent == true) Then
        Set mayEnter = true
    Else
        Set mayEnter = false
    End If
End Module

Module DisplayResult(mayEnter)
    If mayEnter == true Then
        Display "Enter"
    Else
        Display "Entry denied"
    End If
End Module
```

### Desk check

| Case | age | hasTicket | hasParentPresent | Evaluation summary | Message |
| --- | --- | --- | --- | --- | --- |
| A | 20 | true | false | adult and ticket -> true | Enter |
| B | 20 | false | true | adult but no ticket -> false | Entry denied |
| C | 15 | true | true | minor, ticket, parent -> true | Enter |
| D | 15 | true | false | minor, ticket, no parent -> false | Entry denied |

### Why parentheses matter

Without parentheses, a mixed AND/OR expression can be read as more than one rule. Parentheses show whether parent presence is required only for minors, and they keep the adult path separate and obvious.

## Debugging and desk-check task solution

### Why the original condition is wrong

```text
score >= 0 OR score <= 100
```

OR is true when either side is true. Almost every number makes at least one side true.

Examples:

- score = 200: `200 >= 0` is true, so the whole OR is true
- score = -20: `-20 <= 100` is true, so the whole OR is true

The condition almost never fails, so invalid scores are accepted.

### Example of a real-world invalid value wrongly accepted

`score = 150` should be invalid for a 0 to 100 score, but the broken condition calls it valid because `150 >= 0` is true.

### Corrected condition

```text
If score >= 0 AND score <= 100 Then
    Display "Valid"
Else
    Display "Invalid"
End If
```

### Desk check of the corrected condition

| score | score >= 0 | score <= 100 | AND result | Output |
| --- | --- | --- | --- | --- |
| -1 | false | true | false | Invalid |
| 0 | true | true | true | Valid |
| 50 | true | true | true | Valid |
| 100 | true | true | true | Valid |
| 101 | true | false | false | Invalid |
