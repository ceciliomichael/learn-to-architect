# Answer to Question 02

**Why use `git switch` instead of `git checkout`?**

Historically, the `git checkout` command was heavily overloaded. It possessed multiple, entirely unrelated responsibilities. Running `git checkout <branch>` would change your active branch. However, running `git checkout <filename>` would discard local changes to a specific file, reverting it to a previous state.

This dual-purpose design violated the principle of separation of concerns and created massive confusion for junior engineers. A simple typo could accidentally wipe out uncommitted file changes instead of switching branches.

To rectify this architectural flaw, modern versions of Git introduced two explicit, highly focused commands:
1. `git switch`: Used exclusively for navigating between branches.
2. `git restore`: Used exclusively for restoring files or discarding local modifications.

Using `git switch` is safer, more semantic, and represents modern enterprise best practices.
