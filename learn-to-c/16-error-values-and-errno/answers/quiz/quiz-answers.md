# Quiz Answers: Error Values and errno

1. **When should errno be inspected?**

   Only after a documented function call and in the circumstances that function defines.

2. **Why set errno to zero before strtol?**

   A successful call need not clear an older value, so zero establishes a known state for a range check.

3. **How does strtol report where parsing stopped?**

   It writes a pointer to the first unconverted character through its end-pointer argument.

4. **Why reject end == text?**

   It means no digits were converted.

5. **Why is atoi a poor validation tool?**

   It cannot distinguish invalid text from a valid zero and has no useful reporting for overflow.

