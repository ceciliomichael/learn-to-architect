# Quiz Answers: Local Storage, Session Storage, and Data Lifetimes

1. **Is browser storage trusted input?**

   No. It can be old, edited, corrupted, or written by another script on the origin.

2. **What is localStorage's lifetime?**

   It persists by origin until cleared or evicted, unlike sessionStorage's tab session lifetime.

3. **Can storage hold secrets safely?**

   No. Origin scripts can read it, and users or extensions may inspect it.

4. **Why version a storage key?**

   Stored shapes outlive deployments and need explicit migration or rejection.

5. **Can storage operations fail?**

   Yes, due to policy, quota, privacy mode, or unavailable storage.

