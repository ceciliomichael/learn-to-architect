# Exercises: Amend and Clean Private History

## Exercise 1: Amend a private commit

1. Create `history-cleanup` with a committed `guide.txt`.
2. Add `tip.txt` and commit with the vague message `stuff`.
3. Add a missing second line to `tip.txt` and stage it.
4. Amend the commit, changing the message to `Add first usage tip`.
5. Confirm history contains the replacement, not two tip commits.

## Exercise 2: Prepare noisy history

1. Add and commit `part-one.txt` with `Add lesson draft`.
2. Add and commit `part-two.txt` with `fixup lesson draft`.
3. Add and commit `names.txt` with the misspelled message `Add nmaes`.
4. Create a safety branch and inspect the graph.

## Exercise 3: Clean three commits

1. Start interactive rebase over the latest three commits.
2. Keep the first, fix up the second into it, and reword the third as `Add names`.
3. Resolve any prompts and complete the rebase.
4. Verify the compact log and compare the final snapshot with the safety branch.
