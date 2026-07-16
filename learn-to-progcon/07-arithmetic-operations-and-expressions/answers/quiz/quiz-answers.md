# Module 07 Quiz Answers

## Answer 1

- `4 + 6 / 2`  
  `6 / 2 = 3`, then `4 + 3 = 7`. Value: **7**

- `(4 + 6) / 2`  
  `4 + 6 = 10`, then `10 / 2 = 5`. Value: **5**

- `8 * 3 - 2 * 5`  
  `8 * 3 = 24`, `2 * 5 = 10`, then `24 - 10 = 14`. Value: **14**

## Answer 2

An **expression** produces a value, such as `price * quantity` or `3 + 4`.

A **complete instruction** performs an action with that value, such as:

```text
SET total = price * quantity
```

or:

```text
DISPLAY total
```

## Answer 3

One correct design:

```text
CONSTANT DISCOUNT_RATE = 0.15
SET originalPrice = 60
SET discountAmount = originalPrice * DISCOUNT_RATE
SET finalPrice = originalPrice - discountAmount
```

Numeric result:

- discount amount: `60 * 0.15 = 9`
- final price: `60 - 9 = 51`

Equivalent one-step form:

```text
SET finalPrice = 60 * (1 - 0.15)
```

Still `51`.

## Answer 4

A grade average often needs a fractional part (for example, `85.5`). Whole-number division can drop that part and misrepresent student performance. Packing whole boxes may intentionally ignore a fraction because you cannot ship a fraction of a sealed box. The problem goal decides which division idea is appropriate.

## Answer 5

Division happens before the full addition, so only `quiz3` is divided by 3. That is not an average of three quizzes.

Correct forms:

```text
SET average = (quiz1 + quiz2 + quiz3) / 3
```

or:

```text
SET sum = quiz1 + quiz2 + quiz3
SET average = sum / 3
```
