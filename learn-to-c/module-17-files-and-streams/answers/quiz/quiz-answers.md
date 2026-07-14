# Quiz Answers: Files and Streams

1. **What does fopen return on failure?**

   It returns a null pointer.

2. **Why can fclose failure matter for output?**

   Buffered data may be written only while flushing or closing, so an earlier fprintf success is not the complete result.

3. **Should feof be used as a pre-read loop condition?**

   No. Attempt the read and inspect its result; end-of-file becomes known only after a read reaches it.

4. **Who normally closes a FILE stream?**

   The code that owns the successfully opened stream, according to the API's ownership contract.

5. **When should binary mode be used?**

   When exact stored bytes matter and text-mode translation must not occur.

