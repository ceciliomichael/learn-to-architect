# Module 09 Quiz Answers

## Answer 1

```text
B
```

A module is a named group of steps that does one job. In this design course, it is a conceptual unit. Later, in a language like Python, a similar idea often becomes a function.

## Answer 2

```text
C
```

A hierarchy chart shows structure: which modules exist and which module calls which other module. It is not a replacement for detailed pseudocode or formulas.

## Answer 3

```text
B
```

After a called module finishes, control returns to the caller. Main then continues with the next step, which is the call to `ConvertToFahrenheit`.

## Answer 4

```text
C
```

`CalculateAttendancePercent` names a single clear job. Vague names like `DoThings`, `Process`, or `Module2` hide meaning and invite mixed responsibilities.

## Answer 5

```text
B
```

If `DisplayAverage` needs an already calculated average, the design should show that the module receives that value as data it needs. That is the conceptual role of a parameter.
