# Exercise Solutions: Repeat with While Loops

```python
count = 5
while count >= 1:
    print(count)
    count -= 1
print("Go")

answer = ""
while answer != "yes" and answer != "no":
    answer = input("Yes or no? ").strip().lower()

text = input("Nonnegative whole number: ").strip()
while not text.isdecimal():
    text = input("Digits only: ").strip()
number = int(text)

attempts = 0
while attempts < 3:
    if input("Code: ") == "open":
        print("Accepted")
        break
    attempts += 1
else:
    print("No attempts remain")
```

Every continuing path either changes state or intentionally waits for new input.
