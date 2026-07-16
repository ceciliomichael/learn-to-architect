# Module 13 Quiz Answers

## Answer 1

```text
weight >= 5 AND weight <= 12
```

Both ends are inclusive, so 5 and 12 are accepted. AND is required because both limits must hold at the same time.

## Answer 2

```text
B
```

`score >= 90` is false. `score >= 80` is true, so the design displays B and skips the later branches.

## Answer 3

OR makes the condition true when either side is true. Almost every age is either at least 13 or at most 17. A teen range needs AND:

```text
age >= 13 AND age <= 17
```

## Answer 4

Either style can work. Nesting matches the story well because member status is decided first, then the cart total matters only for members. A multi-way chain with compound conditions is also clear.

Nested design:

```text
IF isMember = true THEN
    IF cartTotal >= 50 THEN
        Set discount = 0.15
    ELSE
        Set discount = 0.05
    END IF
ELSE
    Set discount = 0
END IF
```

Multi-way design:

```text
IF isMember = true AND cartTotal >= 50 THEN
    Set discount = 0.15
ELSE IF isMember = true THEN
    Set discount = 0.05
ELSE
    Set discount = 0
END IF
```

Order still matters in the multi-way form. The higher member discount must be tested before the lower member discount.

## Answer 5

For weight 20:

```text
Medium
```

Weight 20 is greater than 5, so Small is skipped. Weight 20 is less than or equal to 20, so Medium runs.

For weight 20.1:

```text
Large
```

Weight 20.1 fails every "at most" band, so the final ELSE runs.
