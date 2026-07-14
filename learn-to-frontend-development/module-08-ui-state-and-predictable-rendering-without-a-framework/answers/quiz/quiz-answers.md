# Quiz Answers: UI State and Predictable Rendering without a Framework

1. **Why use one explicit state value?**

   Transitions become inspectable and rendering can derive visible output from known data.

2. **What is derived state?**

   A value computed from existing state, such as a filtered list, which usually should not be stored separately.

3. **Why make state readonly?**

   It encourages deliberate replacement instead of hidden mutation.

4. **What can replaceChildren affect?**

   Focus and node-local state inside the replaced region, so the render boundary must be chosen carefully.

5. **What does predictable rendering require?**

   The same state and environment should produce the same intended view.

