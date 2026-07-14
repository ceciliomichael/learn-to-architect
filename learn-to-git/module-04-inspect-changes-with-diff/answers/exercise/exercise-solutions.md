# Exercise Solutions: Inspect Changes with Diff

## Exercise 1

After editing:

```text
git status
git diff
git add notes.txt
git diff
git diff --staged
```

Plain diff becomes empty because the working tree and index match. Staged diff shows what the index adds relative to `HEAD`.

## Exercise 2

After the later edit:

```text
git status
git diff
git diff --staged
```

Plain diff shows the later unstaged line. Staged diff shows the earlier line already copied into the index.

## Exercise 3

```text
git add notes.txt
git diff --staged -- notes.txt
git commit -m "Explain diff views"
git diff HEAD^ HEAD
```

The final comparison should show both lines added by the commit.
