# Module 13 Quiz

## Question 1

Write a condition that is true when `weight` is between 5 and 12 inclusive.

## Question 2

What is displayed?

```text
Set score = 85

IF score >= 90 THEN
    Display "A"
ELSE IF score >= 80 THEN
    Display "B"
ELSE IF score >= 70 THEN
    Display "C"
ELSE
    Display "Below C"
END IF
```

## Question 3

Why is this range condition almost always a mistake?

```text
IF age >= 13 OR age <= 17 THEN
    Display "Teen"
END IF
```

## Question 4

A store rule says:

- Members with cart totals of 50 or more get 15 percent off.
- Other members get 5 percent off.
- Non-members get 0 percent off.

Should you use nesting, a multi-way chain, or either? Explain briefly and write one correct pseudocode design.

## Question 5

This design classifies package weight. What does it display for weight 20? What does it display for weight 20.1?

```text
IF weight <= 0 THEN
    Display "Invalid"
ELSE IF weight <= 5 THEN
    Display "Small"
ELSE IF weight <= 20 THEN
    Display "Medium"
ELSE
    Display "Large"
END IF
```

Then read the [quiz answers](../answers/quiz/quiz-answers.md).
