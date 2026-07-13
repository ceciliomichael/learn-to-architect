# Challenge 01 Solution: Detached HEAD Investigation

To safely travel back in time, investigate an older state of your codebase, and return to the present day, you must interact carefully with the HEAD pointer.

## Step-by-Step Execution

### 1. Locate the Target Hash
First, you need to view the commit history to find the receipt number (hash) of the target commit.

```bash
git log --oneline
```
*   `git`: Invokes the Git executable.
*   `log`: Instructs Git to display the history of commits.
*   `--oneline`: A formatting flag that compresses each commit log into a single line, displaying only the short hash and the commit message for maximum readability.

### 2. Enter the Detached HEAD State
Once you identify the hash (for example, `a1b2c3d`), you instruct Git to detach the HEAD pointer from your current branch and point it directly at that historical snapshot.

```bash
git checkout a1b2c3d
```
*   `git`: Invokes the Git executable.
*   `checkout`: The command responsible for updating files in the working tree to match the version in the index or the specified tree.
*   `a1b2c3d`: The specific hexadecimal hash of the commit you wish to visit.

**Analogy:** Imagine your repository is a library. Normally, the librarian (HEAD) is updating the main index book. When you run this command, you ask the librarian to stop looking at the index book and instead go stand next to a specific, dusty old book on a shelf in the back. You are now "detached" from the main timeline.

### 3. Verify and inspect the historical state

```bash
git status
git log -1 --oneline
```

`git status` reports that `HEAD` is detached, while `git log -1 --oneline` confirms the exact historical commit being inspected. You can now open the project files and run read-only tests without creating commits.

### 4. Return to the Present
After you have finished reading the old code, you must bring the librarian back to the active index book to resume normal development.

```bash
git switch main
```
*   `git`: Invokes the Git executable.
*   `switch`: A modern, explicit command introduced in Git to switch branches safely.
*   `main`: The name of your primary branch.

By executing this, the HEAD pointer reattaches to the `main` branch, and your working directory reflects the present day. Run `git status` once more to verify that Git reports `On branch main`.
