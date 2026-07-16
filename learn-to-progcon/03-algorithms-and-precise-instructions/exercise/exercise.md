# Module 03 Exercises

Complete these tasks with paper or a text editor. No programming language is required.

## Warm-up: Repair a vague algorithm

Here is a vague method for a shop total:

```text
Get the stuff.
Work out the money.
Tell the person.
```

1. Rewrite it as an ordered, precise, finite algorithm that:
   - inputs a price and a quantity
   - computes subtotal as price * quantity
   - outputs the subtotal
   - stops
2. Hand-check with price `4` and quantity `5`. State the expected output.

## Guided exercise: From word problem to steps

Word problem:

```text
Read a student's three quiz scores. Calculate the average. If the average is 70 or higher, show "Ready for next unit". Otherwise show "Needs practice".
```

Follow these steps:

1. List the inputs.
2. List the outputs that might appear (there are two possible messages).
3. Write a complete numbered algorithm that is ordered, precise, and finite.
4. Hand-check with scores `60`, `70`, and `80`. Show the average and the message.
5. Hand-check with scores `50`, `55`, and `60`. Show the average and the message.

## Independent exercise: Write and compare

Create algorithms for both problems below. Each algorithm must be ordered, precise, and finite. Include a stop.

**Problem A: Temperature conversion helper**

```text
Read a Celsius temperature. Convert it to Fahrenheit using F = (C * 9/5) + 32. Show the Fahrenheit value.
```

**Problem B: Shipping cost**

```text
Read an order total. If the order total is greater than or equal to 40, shipping is 0. Otherwise shipping is 6. Show the shipping cost only.
```

Requirements:

1. Write Algorithm A with named values.
2. Write Algorithm B with named values.
3. Hand-check Algorithm A with Celsius `10`. State the Fahrenheit result.
4. Hand-check Algorithm B twice: order total `40` and order total `39.99`.
5. In two or three sentences, explain why Algorithm B's decision step must be precise about "greater than or equal to 40" rather than saying "around 40".

## Debugging / desk-check task

A learner wrote this algorithm for "total with 10% discount when quantity is at least 5":

```text
1. Input price
2. Input quantity
3. total = price * quantity
4. If quantity is big, make it cheaper
5. Show something
```

1. List at least four problems with this algorithm using the ideas from the lesson (order, precision, finite end, clear output, testability).
2. Rewrite a correct algorithm.
3. Desk-check your rewrite with price `3` and quantity `5`. State the expected output.
4. Desk-check your rewrite with price `3` and quantity `4`. State the expected output.

## Completion checklist

- [ ] I rewrote vague shop steps into a precise algorithm and checked it.
- [ ] I converted the quiz-average word problem into steps with two hand-checks.
- [ ] I wrote algorithms for temperature conversion and shipping.
- [ ] I explained why vague decision wording is dangerous.
- [ ] I repaired the discount algorithm and verified two test cases.

When you have made a real attempt, compare your work with the [exercise solutions](../answers/exercise/exercise-solutions.md).
