# Exercises: Resolve Merge Conflicts

## Exercise 1: Create a controlled conflict

1. Create a new `conflict-practice` repository with `color.txt` containing `Color: blue` and commit it.
2. Create `choose-green`, change the line to `Color: green`, and commit.
3. Switch to `main`, change the same line to `Color: red`, and commit.
4. Inspect the diverging graph.
5. Merge `choose-green` into `main`.

## Exercise 2: Inspect and abort

1. Run status and diff during the conflict.
2. Identify the current and incoming sections.
3. Abort the merge.
4. Confirm that status is clean and `color.txt` has the main branch version.

## Exercise 3: Resolve deliberately

1. Start the merge again.
2. Replace the entire conflicted line and all markers with `Color: purple`.
3. Stage the resolution.
4. Inspect status and staged diff.
5. Finish the merge and inspect the graph.
