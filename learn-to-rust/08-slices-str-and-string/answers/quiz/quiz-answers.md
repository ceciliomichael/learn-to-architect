# Quiz Answers: Slices, str, and String

1. `String`.
2. `&str`.
3. A byte position is not necessarily a complete Unicode scalar value, and character lookup would not be constant time.
4. Byte offsets that must lie on UTF-8 boundaries.
5. No. It borrows consecutive elements.
