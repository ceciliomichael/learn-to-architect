# Quiz Answers: Unit Testing Browser Logic

1. **What belongs in a unit test?**

   A small behavior with controlled inputs and observable output.

2. **Why separate DOM I/O from logic?**

   Pure logic is faster and easier to test across boundary cases.

3. **What should a test name describe?**

   The behavioral rule and condition, not an implementation method name alone.

4. **Should tests depend on order?**

   No. Each test establishes and cleans its own state.

5. **Do unit tests replace browser tests?**

   No. They cannot prove integration with real DOM and browser behavior.

