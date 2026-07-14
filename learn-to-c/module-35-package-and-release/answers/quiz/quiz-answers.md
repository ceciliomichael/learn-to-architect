# Quiz Answers: Package and Release C Programs

1. **Why report a version?**

   To connect behavior and bug reports to one release.

2. **What belongs in build instructions?**

   Supported tools, language mode, dependencies, configure, build, test, install, and run steps.

3. **Why rebuild from the archive?**

   To catch missing files, hidden workspace assumptions, and incorrect instructions.

4. **What does a checksum show?**

   Whether retrieved bytes match the released artifact, not who published it.

5. **What must stay out of the package?**

   Secrets, credentials, caches, editor state, temporary files, and unrelated outputs.

