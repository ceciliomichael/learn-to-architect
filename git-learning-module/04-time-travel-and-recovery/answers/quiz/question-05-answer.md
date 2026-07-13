# Question 05 Answer

**Question:** When you perform a destructive action like `git reset --hard`, does Git immediately delete the orphaned commits from your hard drive? Explain the lifecycle of this data.

**Exhaustive Explanation:**
No, Git absolutely does not immediately delete data from your hard drive when executing a destructive reset or branch deletion. Git is fundamentally designed around data preservation.

When a commit is orphaned (meaning no branch or tag points to it, and it cannot be reached by traversing backwards from any existing reference), it becomes "unreachable" or "dangling."

**The Garbage Collection Lifecycle:**
1.  **Orphan Status:** The commit blob remains perfectly intact in the `.git/objects` directory on your filesystem.
2.  **Reflog Protection:** By default, the `git reflog` maintains a reference to this commit for 30 days. As long as it is in the reflog, the garbage collector will refuse to touch it.
3.  **True Deletion (`git gc`):** After the reflog entry expires (or if the reflog is manually cleared), the commit is truly dangling. Only then, when Git runs its internal Garbage Collection process (`git gc`), will the raw file blobs finally be deleted from the disk to reclaim space.

This architectural decision means that engineers have a generous grace period to realize they made a catastrophic mistake and recover their code before it is physically overwritten.
