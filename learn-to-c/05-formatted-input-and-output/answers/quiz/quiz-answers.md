# Quiz Answers: Formatted Input and Output

1. **What is stderr for?**

   It carries diagnostics separately from ordinary program output.

2. **Why pass sizeof buffer to fgets?**

   It limits the write to the actual destination capacity.

3. **Does fgets always remove the input newline?**

   No. It stores the newline when it fits, so later text-processing code may need to handle it.

4. **Why is gets unsafe?**

   It cannot receive a destination size and therefore cannot prevent an overflowing write.

5. **What must match a printf conversion?**

   The type of the corresponding variadic argument must satisfy that conversion's contract.

