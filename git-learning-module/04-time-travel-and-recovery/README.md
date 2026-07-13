# Module 04: Time Travel and Recovery

Welcome to the most powerful, and potentially dangerous, module in the Git Academy.

Everything we have done so far has moved forward in time: making commits, branching, merging, and pushing. But software engineering is inherently messy. You will make mistakes. You will deploy code that breaks production. You will accidentally delete files.

Git's greatest strength is its ability to time travel. In this module, we will explore how to view history, safely undo mistakes, and recover from seemingly catastrophic disasters.

---

## 1. Looking at Old Photographs (`git checkout <hash>`)

Imagine you introduced a bug today, but the code was working perfectly three days ago. You want to look at the code exactly as it was three days ago to see what changed.

You can use the `git log` command to find the SHA-1 Hash (the receipt number) of the old commit, and then explicitly teleport your Working Directory to that exact moment in time.

### Syntax Breakdown: `git checkout <hash>`
```bash
git log  # Find the hash, e.g., a1b2c3d
git checkout a1b2c3d
```

### The "Detached HEAD" State
When you run this command, Git will give you a scary-sounding warning: `You are in 'detached HEAD' state.`

Do not panic! The `HEAD` is simply the needle on Git's record player. Normally, the needle rests on a branch name (like `main`). When you check out a specific hash, the needle detaches from the branch and points directly at an old, isolated snapshot.

**The Golden Rule:** You can look around, run your code, and investigate bugs in a detached HEAD state. But **do not make new commits here**. If you want to return to the present day, simply switch back to your branch:
```bash
git switch main
```

---

## 2. The Safe Undo Button (`git revert`)

You pushed a commit to GitHub yesterday, and today you realize it completely broke the login page. You need to undo it immediately.

You might be tempted to delete the commit entirely. **Never do this if the commit is already on the internet.** Deleting history that your teammates have already downloaded will shatter their local repositories.

Instead, use `git revert`.

### The Core Concept: Anti-Matter
`git revert` does not delete history. Instead, it looks at the broken commit, figures out exactly what lines of code were added or removed, and generates a **brand new commit** that does the exact mathematical opposite. It generates anti-matter.

```bash
# Example: Reverting a broken commit
git revert a1b2c3d
```

**Engineering Motivation:** This is the safest, most professional way to undo mistakes in an enterprise environment. The timeline remains perfectly intact, and the audit log clearly shows that a mistake was made and legally corrected.

---

## 3. The Dangerous Time Machine (`git reset`)

If you made a terrible commit, but you **have not** pushed it to GitHub yet, you have permission to rewrite history locally.

`git reset` allows you to physically tear pages out of your Photo Album. It moves the `HEAD` pointer backward in time, completely erasing the commits that came after it.

There are two primary modes:

### A. The Soft Reset (`--soft`)
```bash
git reset --soft HEAD~1
```
* `HEAD~1`: A built-in shortcut meaning "exactly 1 commit before the current HEAD."
* `--soft`: This tears the photograph out of the album, **but leaves the props in your Staging Area**. The code is not lost; it is simply un-committed, allowing you to edit the message or add missing files.

### B. The Hard Reset (`--hard`)
```bash
git reset --hard HEAD~1
```
* `--hard`: This tears the photograph out of the album, kicks all the props out of the Staging Area, and destroys the set in the Workshop. **The code is permanently obliterated.** Use this only when you want to absolutely scorch the earth and destroy your recent local work.

---

## 4. The Ultimate Safety Net (`git reflog`)

You panicked. You ran `git reset --hard` and accidentally destroyed three days of brilliant, un-pushed code. You run `git log` and the commits are completely gone.

Is the code lost forever? **No.**

Git is extremely hesitant to actually delete data. Even when you "destroy" a commit, the data sits hidden in a garbage dump for about 30 days before being truly deleted.

### Syntax Breakdown: `git reflog`
`git reflog` (Reference Log) is the absolute, untouchable diary of every single time the `HEAD` needle moved. Even if you erase history, the reflog recorded the erasure.

```bash
git reflog
```
The output will look like this:
```text
f7e8d9c HEAD@{0}: reset: moving to HEAD~1
a1b2c3d HEAD@{1}: commit: Add brilliant 3 days of work
b4c5d6e HEAD@{2}: commit: Start new feature
```

To rescue your destroyed work, you simply find the hash of the "destroyed" commit in the reflog (`a1b2c3d`), and forcefully reset back to it!
```bash
git reset --hard a1b2c3d
```
Your code is instantly resurrected from the dead. Welcome to mastery.
