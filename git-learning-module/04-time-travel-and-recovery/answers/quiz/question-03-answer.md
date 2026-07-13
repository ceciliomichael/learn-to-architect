# Question 03 Answer

**Question:** Explain the precise architectural difference between executing a `git reset --soft` and a `git reset --hard`.

**Exhaustive Explanation:**
To understand `git reset`, you must understand Git's three-tree architecture: the Commit History, the Staging Area (Index), and the Working Directory. Both commands move the `HEAD` pointer backward in the Commit History, but they treat the other two trees vastly differently.

**1. `git reset --soft`**
*   **Action:** Moves the `HEAD` pointer to an older commit.
*   **Staging Area:** Untouched. All the changes from the "undone" commits are left perfectly preserved and staged, ready to be immediately committed again.
*   **Working Directory:** Untouched. Your actual files on disk do not change.
*   **Use Case:** You made a typo in a commit message, or you want to squash several recent commits together. It safely rewrites history without deleting any code.

**2. `git reset --hard`**
*   **Action:** Moves the `HEAD` pointer to an older commit.
*   **Staging Area:** Obliterated. Git forces the Staging Area to perfectly match the target older commit. Any currently staged files are wiped.
*   **Working Directory:** Obliterated. Git forces your actual files on disk to perfectly match the target older commit. Any uncommitted work, and any work in the "undone" commits, is violently discarded.
*   **Use Case:** Your recent local work is completely unsalvageable, and you need a pristine slate matching a known good historical state. It is highly destructive.
