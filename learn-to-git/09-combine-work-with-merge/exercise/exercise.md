# Exercises: Combine Work with Merge

Use `branch-practice` from Module 08.

## Exercise 1: Perform a fast-forward

1. Switch to `main` with a clean working tree.
2. Inspect the graph and confirm `story-middle` is ahead.
3. Merge `story-middle` into `main`.
4. Inspect the graph and explain which name moved.
5. Delete the merged branch safely.

## Exercise 2: Prepare diverging work

1. On `main`, add `Ending.` to `story.txt` and commit.
2. Create `add-title` from `HEAD^` rather than from the latest commit: `git switch -c add-title HEAD^`.
3. Create `title.txt` with `A Short Story` and commit it.
4. Draw and inspect the diverging graph.

## Exercise 3: Perform a three-way merge

1. Switch to `main`.
2. Merge `add-title`.
3. Inspect status, files, graph, and newest commit.
4. Confirm the newest commit has two parents.
