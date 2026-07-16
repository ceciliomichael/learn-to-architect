# Module 23 Exercise Solutions

This solution walks through **Option A: Grade calculator** as a complete sample. If you chose Option B or C, your content will differ, but the same deliverable quality is expected.

## Warm-up solution

**Choice:** Option A

**Problem statement:** Compute the average and highest of three quiz scores and print Pass or Review.

**Inputs:** three scores

**Processes:** store scores, average, maximum, compare average to 75

**Outputs:** scores, average, highest, Pass or Review

Removed from minimum version: saving to a file, class ranking charts, graphical windows.

## Guided exercise solution (design pack)

### Algorithm

1. Start the program.
2. Read three scores into a list.
3. Compute the average with a helper.
4. Compute the highest score with a helper.
5. Display the scores.
6. Display the average and highest score.
7. If average >= 75, display Pass. Else display Review.
8. End.

### Pseudocode

```text
MODULE readScores(count)
    SET scores = empty list
    FOR i FROM 1 TO count
        INPUT value
        APPEND value to scores
    END FOR
    RETURN scores
END MODULE

MODULE averageOf(scores)
    SET total = 0
    FOR each score in scores
        SET total = total + score
    END FOR
    RETURN total / length of scores
END MODULE

MODULE maximumOf(scores)
    SET highest = scores[0]
    FOR each score in scores
        IF score > highest THEN
            SET highest = score
        END IF
    END FOR
    RETURN highest
END MODULE

MODULE main
    SET scores = readScores(3)
    SET avg = averageOf(scores)
    SET high = maximumOf(scores)
    OUTPUT scores
    OUTPUT avg
    OUTPUT high
    IF avg >= 75 THEN
        OUTPUT "Pass"
    ELSE
        OUTPUT "Review"
    END IF
END MODULE
```

### Hierarchy chart

```text
            main
         /    |    \
        /     |     \
 readScores averageOf maximumOf
```

### Flowchart (main path)

```text
[START]
   |
[scores = readScores(3)]
   |
[avg = averageOf(scores)]
   |
[high = maximumOf(scores)]
   |
[OUTPUT scores, avg, high]
   |
  / \
 /   \ avg >= 75?
 \   /
  \ /
yes|   \no
   |    \
[Pass] [Review]
   |    /
   +---+
   |
 [END]
```

### Trace (normal case)

Inputs: 80, 90, 70

| Step | scores | avg | high | message |
| --- | --- | --- | --- | --- |
| after read | [80, 90, 70] |  |  |  |
| after average |  | 80 |  |  |
| after maximum |  | 80 | 90 |  |
| after decision |  | 80 | 90 | Pass |

## Independent exercise solution (implementation and tests)

```python
def read_scores(count):
    scores = []
    for i in range(count):
        value = float(input("Score: "))
        scores.append(value)
    return scores


def average_of(scores):
    total = 0.0
    for score in scores:
        total = total + score
    return total / len(scores)


def maximum_of(scores):
    highest = scores[0]
    for score in scores:
        if score > highest:
            highest = score
    return highest


def main():
    scores = read_scores(3)
    avg = average_of(scores)
    high = maximum_of(scores)
    print("Scores:", scores)
    print("Average:", avg)
    print("Highest:", high)
    if avg >= 75:
        print("Pass")
    else:
        print("Review")


main()
```

### Test log sample

| Case | Inputs | Expected | Actual | Pass? |
| --- | --- | --- | --- | --- |
| Normal | 80, 90, 70 | avg 80, high 90, Pass | avg 80, high 90, Pass | Yes |
| Boundary | 75, 75, 75 | avg 75, Pass | avg 75, Pass | Yes |
| Edge | 50, 60, 70 | avg 60, Review | avg 60, Review | Yes |

### Presentation note sample

I chose the grade calculator because it uses lists, loops, functions, and selection without extra features. The helper functions keep averaging and maximum-finding separate from input. One bug I avoided by tracing first was dividing by 3 before all scores were collected. Next I might allow a variable number of scores with a sentinel.

## Debugging / review task solution

Use the lesson checklist on your own project. For the sample above:

1. Functions each have one job: read, average, maximum, main orchestration.
2. Indexes stay inside the list because loops use `for score in scores` or `range(count)` for input only.
3. The input loop runs a fixed number of times and ends.
4. Both Pass and Review branches exist.
5. Outputs match the requirements list.
