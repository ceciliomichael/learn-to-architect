# Challenge 03: The Merge Conflict

**Scenario:**
You and a colleague have independently modified the exact same line of code in a configuration file on two different branches. When you attempt to merge, Git halts the process and asks for human intervention.

**Tasks:**
1. Create a text file and commit an initial line of text on `main`.
2. Create a new branch called `feature-config` and switch to it.
3. Edit the exact same line of text, save the file, and commit the change.
4. Switch back to `main`, edit the same line of text differently, and commit the change.
5. Attempt to merge `feature-config` into `main`.
6. Open the file in an editor, locate the Git conflict markers, resolve the conflict, and finalize the merge.
