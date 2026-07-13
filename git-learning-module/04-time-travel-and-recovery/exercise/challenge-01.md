# Challenge 01: Detached HEAD Investigation

**Scenario:**
A critical bug was reported in production today. The application was working perfectly stable exactly three commits ago. You need to travel back in time to inspect the codebase at that specific moment, run some local tests, and then safely return to the present without breaking anything.

**Objectives:**
1. Find the commit hash for the snapshot that occurred three commits ago.
2. Checkout that specific commit hash to enter a detached HEAD state.
3. Verify your repository is in the detached state and inspect the files.
4. Safely return your working directory to the `main` branch.

**Constraints:**
Do not make any new commits while in the detached HEAD state.
