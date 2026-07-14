# Exercises: Stage the Exact Changes You Want

## Exercise 1: Stage selected files

1. Create `alpha.txt` and `beta.txt` with one line each.
2. Stage only `alpha.txt`.
3. Use status and staged diff to prove the selection.
4. Unstage `alpha.txt` without deleting it.
5. Prove that both files still exist as untracked files.

## Exercise 2: Stage selected hunks

1. Add a line near the start and another line near the end of a tracked file. Put enough unchanged lines between them for Git to show separate hunks.
2. Run interactive add and stage only the first hunk.
3. Inspect plain and staged diff.
4. Commit the first purpose, then stage and commit the second.

## Exercise 3: Record a rename

1. Rename `alpha.txt` to `first.txt` with Git.
2. Inspect status and staged diff.
3. Commit the change with a clear message.
