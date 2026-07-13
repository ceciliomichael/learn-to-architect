# Challenge 02: The Safe Undo

**Scenario:**
You just merged and pushed a feature to the central repository, but a teammate immediately notifies you that your commit broke the user login system. Since the commit is already public on the internet, deleting it from history would corrupt your teammates' local environments. You must apply a safe fix.

**Objectives:**
1. Identify the hash of the broken commit that you just pushed.
2. Generate a new commit that applies the exact mathematical opposite of the broken commit.
3. Verify that the repository history remains intact and the audit log clearly shows the reversal.
