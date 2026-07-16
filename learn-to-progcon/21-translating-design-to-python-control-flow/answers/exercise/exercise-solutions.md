# Module 21 Exercise Solutions

## Warm-up solution

```python
temperature = 24
if temperature > 35:
    print("Extreme heat")
elif temperature > 25:
    print("Hot day")
else:
    print("Mild day")
```

For `24`, output is `Mild day`.

## Guided exercise solution

```python
age_text = input("Enter age: ")
age = int(age_text)

if age < 13:
    print("Child ticket")  # test 10
elif age <= 59:
    print("Adult ticket")  # test 30
else:
    print("Senior ticket")  # test 65
```

## Independent exercise solution

```python
# Read three scores, print average and pass message.
total = 0.0
for count in range(3):
    text = input("Enter score: ")
    score = float(text)
    total = total + score

average = total / 3
print("Average:", average)

if average >= 75:
    print("Pass")
else:
    print("Needs review")
```

## Debugging task solution

```python
count = 1
while count <= 3:
    print(count)
    count = count + 1

score_text = input("Score: ")
score = float(score_text)
if score >= 50:
    print("OK")
```

Fixes:

1. Added `:` after the while condition.
2. Indented the while body.
3. Converted input before comparing as a number.
