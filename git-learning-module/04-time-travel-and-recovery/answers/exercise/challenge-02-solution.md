# Challenge 02 Solution: The Safe Undo

When dealing with a public repository, rewriting history is strictly prohibited. You must use anti-matter to neutralize the mistake.

## Step-by-Step Execution

### 1. Identify the Broken Commit
Find the exact hash of the commit that broke the application.

```bash
git log -n 5
```
*   `git`: Invokes the executable.
*   `log`: Reads the commit history.
*   `-n 5`: Limits the output to the most recent 5 commits, keeping your terminal output concise.

### 2. Apply the Reversal
Assume the broken commit has the hash `bad9876`. You will instruct Git to create a new, opposite commit.

```bash
git revert bad9876
```
*   `git`: Invokes the executable.
*   `revert`: The command that calculates the inverse of the specified commit and applies it.
*   `bad9876`: The exact hash of the commit you want to undo.

### 3. Verify the preserved history

```bash
git log --oneline -n 5
```

The log should contain both the original broken commit and the newer revert commit. This proves that the public history was preserved rather than rewritten.

**Analogy:** Imagine you accidentally poured blue dye into a vat of white paint. You cannot simply travel back in time and prevent the pour (because people have already bought the blue-tinted paint). Instead, you add a calculated amount of yellow dye (the revert) to neutralize the color back to white. The timeline clearly shows both actions, preserving the enterprise audit log.
