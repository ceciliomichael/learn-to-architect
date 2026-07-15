# Exercises: Reset Local History

Use only a disposable repository.

## Exercise 1: Prepare two commits

1. Create `reset-practice` with `count.txt` containing `one` and commit it.
2. Change the content to `two` and commit it.
3. Create `latest-safety` at the latest commit.
4. Record the hashes and inspect the clean state.

## Exercise 2: Compare soft and mixed

1. Soft reset `main` to its parent.
2. Inspect the graph, status, both diffs, and file.
3. Reset hard to `latest-safety` to restore the prepared state.
4. Mixed reset to its parent.
5. Inspect the same evidence and compare it with soft.

## Exercise 3: Observe hard reset safely

1. Return hard to `latest-safety`.
2. Add an uncommitted third line to the tracked file.
3. Inspect and copy that line outside the repository.
4. Hard reset to `HEAD^`.
5. Confirm branch, index, and working tree match the first commit.
