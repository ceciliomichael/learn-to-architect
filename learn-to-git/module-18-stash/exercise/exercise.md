# Exercises: Set Work Aside with Stash

Create `stash-practice` with a committed `draft.txt` containing `Original.`

## Exercise 1: Stash tracked work

1. Change the tracked line to `Tracked draft.`
2. Create untracked `new-draft.txt`.
3. Create a named stash without `-u`.
4. Confirm the tracked file is clean but the untracked file remains.
5. Inspect the stash patch.

## Exercise 2: Apply and drop separately

1. Apply the newest stash.
2. Confirm its change returned and the entry still exists.
3. Restore the working file to clean after inspecting it.
4. Drop that stash explicitly.

## Exercise 3: Include a new file

1. Edit the tracked file and keep `new-draft.txt` untracked.
2. Stash with `-u` and a clear message.
3. Confirm the working tree is clean.
4. Restore it on a new branch with `git stash branch`.
5. Commit the recovered files as one coherent change.
