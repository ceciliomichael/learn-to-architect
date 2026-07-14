# Quiz Answers: Arrays and Length Tracking

1. **What are the valid indexes of an array with count elements?**

   Zero through count minus one.

2. **Does C automatically stop an out-of-bounds array access?**

   No. An out-of-bounds access has undefined behavior and may appear to work.

3. **Where can sizeof array / sizeof array[0] find an array count?**

   Where array still names the actual array object, not in a function parameter adjusted to a pointer.

4. **Why pass a count to an array-processing function?**

   The called function otherwise has no general way to know how many elements are valid.

5. **What type does sizeof produce?**

   It produces a value of type size_t.

