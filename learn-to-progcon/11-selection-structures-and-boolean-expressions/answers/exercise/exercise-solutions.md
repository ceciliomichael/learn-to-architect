# Module 11 Exercise Solutions

## Warm-up solution

1. true (`60 >= 60`)
2. false (`3 < 0` is false)
3. true
4. false (`100 > 100` is false)
5. false
6. arithmetic
7. boolean
8. arithmetic
9. boolean

## Guided exercise solution

### Part A

```text
Display "Enter temperature: "
Input temperature

If temperature < 0 Then
    Display "Freezing warning"
End If

Display "Temperature check finished"
```

Plain-text flowchart:

```text
[Start]
   |
   v
[Input temperature]
   |
   v
[temperature < 0?]
    |         \
   Yes         No
    |           \
    v            \
[Freezing warning]\
    |              \
    +-------+-------+
            |
            v
[Temperature check finished]
            |
            v
          [End]
```

### Part B

```text
Display "Enter score: "
Input score

If score >= 60 Then
    Display "Pass"
Else
    Display "Needs review"
End If
```

Desk check:

| score | Condition | Output |
| --- | --- | --- |
| 72 | true | Pass |
| 45 | false | Needs review |

## Independent exercise solution

### Hierarchy chart

```text
                         Main
                           |
     ----------------------+----------------------
     |           |         |          |          |
DisplayWelcome GetOrder  ApplyPricing DisplayPrice DisplayThanks
```

### Pseudocode

```text
Module Main
    Declare Real price
    Declare Boolean hasCoupon
    Declare Real finalPrice

    Call DisplayWelcome
    Call GetOrder(price, hasCoupon)
    Call ApplyPricing(price, hasCoupon, finalPrice)
    Call DisplayPrice(finalPrice)
    Call DisplayThanks
End Module

Module DisplayWelcome
    Display "Corner Mart Checkout"
End Module

Module GetOrder(price, hasCoupon)
    Display "Enter item price: "
    Input price
    Display "Do you have a coupon (true/false): "
    Input hasCoupon
End Module

Module ApplyPricing(price, hasCoupon, finalPrice)
    If hasCoupon == true Then
        Set finalPrice = price * 0.85
    Else
        Set finalPrice = price
    End If
End Module

Module DisplayPrice(finalPrice)
    Display "Final price: ", finalPrice
End Module

Module DisplayThanks
    Display "Thank you for shopping."
End Module
```

### Decision flowchart for ApplyPricing

```text
        [hasCoupon == true?]
           /            \
         Yes             No
          |               |
          v               v
[final = price * 0.85] [final = price]
          \               /
           \             /
            v           v
             [return]
```

### Desk checks

| price | hasCoupon | finalPrice | Notes |
| --- | --- | --- | --- |
| 20 | true | 17 | 20 * 0.85 |
| 20 | false | 20 | no discount |

## Debugging and desk-check task solution

### Problems in the original

1. `score = 60` looks like assignment, not a comparison. A boolean test should use equality, such as `score == 60`, or a range test such as `score >= 60` for passing.
2. `Then` is missing after the condition in common pseudocode form.
3. `End If` is missing, so it is unclear where the selection ends.
4. `"Always shown?"` is indented under Else in spirit but written without clear structure, so a reader cannot be sure whether it always runs.

### Corrected design for a normal pass rule

If the intent is a standard pass threshold:

```text
Display "Enter score: "
Input score

If score >= 60 Then
    Display "Pass"
Else
    Display "Needs review"
End If

Display "Always shown?"
```

If the original author truly meant "exactly 60 passes," that would be unusual for grades, but the comparison form would be `score == 60`. In school contexts, `>= 60` is the sensible pass rule.

### Should "Always shown?" run for every score?

Yes, based on the question text. Place it after `End If`.

### Desk check of the corrected pass-threshold design

| score | Condition `score >= 60` | Messages |
| --- | --- | --- |
| 60 | true | Pass / Always shown? |
| 59 | false | Needs review / Always shown? |
| 95 | true | Pass / Always shown? |
