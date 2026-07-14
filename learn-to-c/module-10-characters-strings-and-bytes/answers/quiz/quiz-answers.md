# Quiz Answers: Characters, Strings, and Bytes

1. **What marks the end of a C string?**

   A zero-valued char byte, written as '\0'.

2. **Does strlen include the terminator?**

   No. It counts the preceding characters only.

3. **What is the difference between capacity and length?**

   Capacity is available storage; length is the number of characters before the current terminator.

4. **How does snprintf report truncation?**

   A nonnegative return value at least as large as the supplied capacity means the full formatted result did not fit.

5. **Can an arbitrary byte array be passed to %s?**

   Only if it contains a terminator within its accessible bounds and represents the intended string.

