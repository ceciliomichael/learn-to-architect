# Quiz Answers: Arrays, Pointer Arithmetic, and Bounds

1. **How far does pointer + 1 move?**

   It moves to the next object of the pointer's pointed-to type.

2. **May a one-past pointer be formed?**

   Yes, for boundary calculations and comparisons within that array, but it may not be dereferenced.

3. **Where are pointer ordering comparisons defined?**

   For pointers into the same array object, including its one-past boundary.

4. **How are values[index] and *(values + index) related?**

   They designate the same element when the index is in bounds.

5. **What information should accompany an array pointer?**

   A count or end pointer that defines the accessible range.

