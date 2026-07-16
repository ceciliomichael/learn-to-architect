# Module 14 Quiz Answers

## Answer 1

Any three valid advantages are fine. Common answers:

1. You write the repeated steps once instead of many copies.
2. A fix in the body improves every repetition.
3. The same design can handle different numbers of repetitions.
4. The stopping rule is stated clearly in the condition.

## Answer 2

```text
2
3
4
5
```

`count` starts at 2. The loop runs while `count <= 5`, displays the current count, then adds 1. When count becomes 6, the condition fails.

## Answer 3

A priming read is an input performed before the WHILE condition is tested for the first time.

This design needs it so:

1. `score` has a value for the first condition check.
2. Real scores can be added in the body.
3. The stop value -1 can be read and tested without being added as data.

The input at the bottom of the body is the update that prepares the next check.

## Answer 4

The body displays `battery` but never changes it, so `battery > 0` stays true forever.

Fix:

```text
Set battery = 3

WHILE battery > 0
    Display battery
    Set battery = battery - 1
END WHILE
```

## Answer 5

A WHILE condition is checked before the body on every potential pass, including the first.

If the condition is false on the first check, the body never runs. The design continues with the steps after the loop.
