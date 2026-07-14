# Quiz Answers: Libraries, ABI Contracts, and Foreign Interfaces

1. **What does a public header define?**

   The source-level names, types, constants, and ownership rules.

2. **What can affect an ABI?**

   Calling conventions, layout, alignment, symbols, compiler settings, and runtime libraries.

3. **Why use opaque handles?**

   They hide private layout and reduce public ABI exposure.

4. **Why use an extern C guard?**

   It requests C linkage from C++ while remaining valid C.

5. **What ownership facts matter at FFI boundaries?**

   Creation, lifetime, borrowing, mutation, release, and the matching allocator.

