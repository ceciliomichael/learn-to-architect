# Exercise Solutions: Reset Local History

## Exercise 1

```text
mkdir reset-practice
cd reset-practice
git init
git add count.txt
git commit -m "Set count to one"
git add count.txt
git commit -m "Set count to two"
git branch latest-safety
git log --oneline --decorate
git status
```

Edit the file to each stated value before staging.

## Exercise 2

```text
git reset --soft HEAD^
git status
git diff
git diff --staged
git log --oneline --decorate --all
git reset --hard latest-safety
git reset --mixed HEAD^
git status
git diff
git diff --staged
```

Soft leaves the change staged. Mixed leaves the same file content but makes the change unstaged.

## Exercise 3

```text
git reset --hard latest-safety
git diff
git reset --hard HEAD^
git status
git log --oneline --decorate --all
```

Add and separately copy the third line before the hard reset. Afterward, `main` and the tracked file match the first commit. `latest-safety` still names the second commit.
