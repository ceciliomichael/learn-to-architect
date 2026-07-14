# Exercise Solutions: Booleans and Conditions

```python
score = int(input("Score: "))
if score >= 90:
    print("Excellent")
elif score >= 75:
    print("Good")
elif score >= 60:
    print("Passing")
else:
    print("Needs review")

is_active = True
role = "editor"
if is_active and (role == "owner" or role == "editor"):
    print("Access allowed")

answer = input("Answer: ").strip()
if not answer:
    print("Answer required")

denominator = 0
if denominator != 0:
    print(10 / denominator)
else:
    print("Cannot divide by zero")
```

Higher score boundaries must come first or a broad lower condition would capture them.
