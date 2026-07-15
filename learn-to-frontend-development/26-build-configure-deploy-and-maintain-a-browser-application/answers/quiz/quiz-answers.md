# Quiz Answers: Build, Configure, Deploy, and Maintain a Browser Application

1. **Can browser environment variables contain secrets?**

   No. Values embedded in browser assets are available to users.

2. **What should a production build check?**

   Strict types, tests, asset paths, size, source maps, headers, configuration, and the exact built artifact.

3. **Why test under the deployed base path?**

   Root-relative assumptions may fail outside local root hosting.

4. **What does rollback require?**

   A known previous artifact and compatible server, data, and cache behavior.

5. **Why review dependency upgrades?**

   Browser dependencies execute in the user-facing trust boundary.

