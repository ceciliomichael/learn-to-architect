# Quiz Answers: Files, Blobs, Object URLs, and Downloads

1. **Does accept or MIME type prove a safe file?**

   No. They are hints and metadata; trusted processing validates actual content.

2. **Why limit file size before reading?**

   To bound memory, processing time, and user mistakes.

3. **What is an object URL?**

   A temporary origin-scoped URL referring to a Blob or File.

4. **Why revoke object URLs?**

   To release the browser-held reference when no longer needed.

5. **Does selecting a file upload it?**

   No. Upload requires an explicit request.

