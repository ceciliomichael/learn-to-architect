# Quiz Answers: Revert Published Commits

1. No. It adds a new commit at the branch tip.
2. It preserves hashes and history that other contributors may already use.
3. Its patch with `git show`, plus the surrounding graph and current status.
4. `git revert --continue`.
5. A merge has multiple parents, so you must choose the mainline parent whose side should be kept.
