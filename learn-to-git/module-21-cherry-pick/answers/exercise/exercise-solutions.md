# Exercise Solutions: Copy a Commit with Cherry-Pick

## Exercise 1

```text
mkdir pick-practice
cd pick-practice
git init
git add base.txt
git commit -m "Add base"
git switch -c future
git add feature.txt
git commit -m "Add reusable feature"
git switch main
git add main.txt
git commit -m "Add main note"
git log --graph --oneline --decorate --all
```

Create each file before staging it.

## Exercise 2

```text
git status
git show SOURCE_HASH
git cherry-pick -x SOURCE_HASH
git show --format=fuller HEAD
```

The message should include the original commit reference.

## Exercise 3

```text
git log --graph --oneline --decorate --all
git show SOURCE_HASH
git show HEAD
```

The content change can match. The parent and committer data differ, so the commit identities differ.
