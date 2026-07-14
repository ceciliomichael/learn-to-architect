# Exercises: Rebase a Private Branch

## Exercise 1: Create diverging history

1. Create `rebase-practice` with committed `base.txt`.
2. Create `topic` and make two commits adding `topic-one.txt` and `topic-two.txt`.
3. Switch to `main`, add and commit `main-update.txt`.
4. Inspect the graph and record the two topic hashes.

## Exercise 2: Rebase safely

1. Switch to `topic` with a clean tree.
2. Create `topic-before-rebase` as a safety branch.
3. Rebase onto `main`.
4. Inspect the graph and compare new topic hashes with the recorded ones.
5. Confirm all three added files exist on `topic`.

## Exercise 3: Verify integration

1. Switch to `main`.
2. Merge `topic`.
3. Confirm the merge fast-forwards.
4. Inspect the graph and safely delete `topic`.
