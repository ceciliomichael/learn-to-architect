# Exercises: Copy a Commit with Cherry-Pick

## Exercise 1: Prepare separate branches

1. Create `pick-practice` with a base commit.
2. Create `future`, add `feature.txt`, and commit it.
3. Return to `main`, add a different `main.txt`, and commit it.
4. Inspect the diverging graph and copy the feature commit hash.

## Exercise 2: Pick one change

1. Confirm `main` is current and clean.
2. Inspect the selected feature commit.
3. Cherry-pick it with `-x`.
4. Confirm `feature.txt` exists on main.
5. Inspect the new commit's hash, parent, and message.

## Exercise 3: Compare source and copy

1. Show the source and new commit side by side in the graph.
2. Compare their patches.
3. Explain why their patches can match while their hashes differ.
