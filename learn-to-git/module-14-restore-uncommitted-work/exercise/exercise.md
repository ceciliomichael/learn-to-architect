# Exercises: Restore Uncommitted Work

Create a disposable `restore-practice` repository with one committed `notes.txt` containing `Saved line.`

## Exercise 1: Unstage but keep

1. Add `Useful draft.` to the file and stage it.
2. Inspect the staged diff.
3. Unstage it without changing the working file.
4. Inspect status and plain diff to prove the text remains.

## Exercise 2: Discard a known practice edit

1. Copy `Useful draft.` somewhere outside the repository for safety.
2. Restore `notes.txt` from the index.
3. Confirm the working tree is clean and only `Saved line.` remains.

## Exercise 3: Preview untracked cleanup

1. Create untracked `temporary.txt` and an untracked `output` folder with a file.
2. Preview clean without directories.
3. Preview clean including directories.
4. Confirm both previews changed nothing.
5. Remove the practice paths with your normal file tools.
