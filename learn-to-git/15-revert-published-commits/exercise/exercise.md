# Exercises: Revert Published Commits

## Exercise 1: Prepare shared-style history

1. Create `revert-practice` with `settings.txt` containing `mode=safe` and commit it.
2. Change the line to `mode=unsafe` and commit with `Enable unsafe mode`.
3. Add `owner=team` in a separate commit.
4. Inspect the graph and both recent patches.

## Exercise 2: Revert the middle change

1. Copy the hash of `Enable unsafe mode`.
2. Revert that commit.
3. Confirm the file contains `mode=safe` and still contains `owner=team`.
4. Inspect the graph and the revert patch.

## Exercise 3: Reverse the decision

1. Revert the new revert commit.
2. Confirm unsafe mode returns and the owner remains.
3. Explain why none of the earlier commits disappeared.
