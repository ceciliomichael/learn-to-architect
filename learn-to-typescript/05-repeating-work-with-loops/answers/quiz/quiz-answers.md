# Module 05 Quiz Answers

## Answer 1

1. `let count = 1` creates the counter once.
2. `count <= 3` is checked before each repetition.
3. `count = count + 1` updates the counter after each repetition.

## Answer 2

```text
3
2
1
```

After printing `1`, the update makes the number `0`. The condition `0 >= 1` is false, so the loop stops.

## Answer 3

The count moves downward. Every value it reaches, including zero and negative values, still satisfies `count <= 3`. The update should add one so the count eventually becomes `4`.

## Answer 4

Create a running total before the loop. It must keep its value between repetitions and remain available after the loop. Creating it inside would reset it each time.

## Answer 5

`continue` skips the rest of the current repetition and moves to the next one. `break` stops the whole loop.
