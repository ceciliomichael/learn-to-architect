# Question 02 Answer

**Question:** Why is the `git revert` command fundamentally safer than `git reset` when dealing with commits that have already been pushed to a remote repository?

**Exhaustive Explanation:**
The fundamental rule of distributed version control is that you must never alter public history. When you push a commit to a remote server like GitHub, your teammates fetch that exact mathematical history onto their local machines.

If you use `git reset` to "erase" a pushed commit, you are physically tearing pages out of the repository's history book. When your teammates attempt to sync with the server, their local Git clients will detect a catastrophic timeline divergence. Their local history has the commit, but the server's history does not. This results in horrific merge conflicts, broken local environments, and massive productivity loss across the engineering team.

**The Anti-Matter Solution:**
`git revert` does not alter existing history. Instead, it analyzes the delta (the exact lines of code added or removed in the broken commit) and generates a brand new, sequential commit that applies the exact inverse operations.

By using `revert`, you simply add a new page to the end of the history book. When teammates pull the latest changes, they naturally receive the "reversal" commit, and their timelines advance cleanly without conflict. Furthermore, the enterprise audit trail remains intact, proving exactly when the mistake occurred and when it was formally corrected.
