# Module 04 Quiz Answers

## Answer 1

Every comparison produces a boolean. For the shown values, the results are `true`, `false`, and `true`.

## Answer 2

```text
B
```

The first condition is false. The second is true, so its block runs and the remaining chain is skipped.

## Answer 3

- `&&` is true when both sides are true.
- `||` is true when at least one side is true.
- `!` reverses a boolean value.

## Answer 4

A score of `95` already satisfies `score >= 60`, so the first branch runs and the `>= 90` branch is never reached. Higher or more specific thresholds should appear first.

## Answer 5

```typescript
age >= 18 && hasPermission
```

Both requirements must be true, so `&&` matches the rule.
