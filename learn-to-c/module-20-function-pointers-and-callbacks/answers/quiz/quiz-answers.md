# Quiz Answers: Function Pointers and Callbacks

1. **What defines a function pointer's compatibility?**

   Its pointed-to function's return type and parameter types, including relevant qualifiers and variadic status.

2. **What should a qsort comparator return for equal elements?**

   Zero.

3. **Why avoid return left - right?**

   The subtraction can overflow for valid int values and cause undefined behavior.

4. **What do qsort's void pointers designate?**

   They designate the two array elements currently being compared.

5. **Who defines a callback's result contract?**

   The API receiving and calling the callback.

