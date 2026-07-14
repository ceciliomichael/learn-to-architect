# Exercise Solutions: Stage the Exact Changes You Want

## Exercise 1

After creating both files:

```text
git add alpha.txt
git status
git diff --staged
git restore --staged alpha.txt
git status
```

Both files should be untracked. Their content remains on disk.

Before the rename exercise, add and commit them:

```text
git add alpha.txt beta.txt
git commit -m "Add staging practice files"
```

## Exercise 2

```text
git diff
git add -p notes.txt
git diff
git diff --staged
git commit -m "Describe the first change"
git add notes.txt
git commit -m "Describe the second change"
```

Choose `y` for the first hunk and `n` for the second. If Git combines them, choose `s`. Your messages should describe the actual edits.

## Exercise 3

```text
git mv alpha.txt first.txt
git status
git diff --staged
git commit -m "Rename alpha notes to first notes"
```
