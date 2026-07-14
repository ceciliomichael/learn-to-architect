# Quiz Answers: Dynamic Memory and Ownership

1. **What does malloc return on failure?**

   It returns a null pointer.

2. **Why is malloc not normally cast in C?**

   void * converts to an object pointer in C, and a cast can hide a missing or incorrect declaration.

3. **What must be checked before count * element_size?**

   That count is no greater than SIZE_MAX divided by element_size, plus any application-specific maximum.

4. **May an object be read after free?**

   No. Its lifetime has ended, so pointers that designated it are dangling.

5. **Does setting one pointer to NULL remove all aliases?**

   No. Other copies of the old address remain dangling.

