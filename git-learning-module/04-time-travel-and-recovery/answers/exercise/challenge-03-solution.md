# Challenge 03 Solution: Reflog Resurrection

The reference log is your ultimate safety net in Git, recording every movement of the HEAD pointer regardless of branch history.

## Step-by-Step Execution

### 1. Simulate the Disaster
If you accidentally destroy your work using a hard reset, the commits vanish from standard history.

```bash
git reset --hard HEAD~3
```
*   `git`: Invokes the executable.
*   `reset`: The command to move the HEAD pointer backward.
*   `--hard`: The destructive flag that forces the working directory and staging area to match the older commit, wiping out recent changes.
*   `HEAD~3`: A relative reference meaning "three commits before the current HEAD".

### 2. Locate the Lost Hash
Your recent commits are no longer accessible via `git log`. You must query the reference log.

```bash
git reflog
```
*   `git`: Invokes the executable.
*   `reflog`: Outputs the diary of HEAD pointer movements.

In the output, you will see a chronological list of actions. Find the entry from right before you executed the destructive reset. It will have a hash, for example, `f7e8d9c`.

### 3. Resurrect the Code
You will now violently yank the HEAD pointer back to the lost hash, restoring your code.

```bash
git reset --hard f7e8d9c
```
*   `git`: Invokes the executable.
*   `reset`: The command to move the HEAD.
*   `--hard`: Forces your working directory to immediately match the resurrected commit.
*   `f7e8d9c`: The hash you discovered in the reflog.

### 4. Verify the restoration

```bash
git status
git log --oneline -n 5
```

Confirm that the recovered commits are visible in the log and open the restored files to verify that the lost work is present in the Working Directory.

**Analogy:** The reflog is like a hidden security camera in a bank. Even if a thief (the hard reset) breaks in and deletes the official transaction ledger (`git log`), the security camera (`git reflog`) silently recorded exactly what was in the vault before the robbery. You use the camera footage to instantly restore the vault to its exact prior state.
