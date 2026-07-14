# Exercises: Reflog, Detached HEAD, and Recovery

Use the disposable `reset-practice` repository.

## Exercise 1: Read movements

1. Run the normal graph log.
2. Run the reflog.
3. Find an entry created by a reset from Module 16.
4. Inspect the commit named by that entry.
5. Create `reflog-recovery` at it without moving `main`.

## Exercise 2: Work while detached

1. Switch detached to the first commit in the repository.
2. Confirm no current branch name is printed.
3. Create `experiment.txt` and commit it.
4. Inspect the graph for all references and the reflog.

## Exercise 3: Attach the experiment

1. While on the detached experiment commit, create and switch to `saved-experiment`.
2. Confirm the branch name.
3. Switch to `main`.
4. Prove the experiment commit is still reachable from `saved-experiment`.
