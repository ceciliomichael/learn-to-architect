# Exercise Solutions: Set Work Aside with Stash

## Setup

```text
mkdir stash-practice
cd stash-practice
git init
git add draft.txt
git commit -m "Add original draft"
```

## Exercise 1

After editing and creating the new file:

```text
git status
git stash push -m "tracked draft"
git status
git stash list
git stash show -p "stash@{0}"
```

`new-draft.txt` remains untracked because the stash command did not use `-u`.

## Exercise 2

```text
git stash apply "stash@{0}"
git status
git stash list
git restore draft.txt
git stash drop "stash@{0}"
git stash list
```

Apply leaves the entry in the list. Drop removes it after you no longer need it.

## Exercise 3

After editing both paths:

```text
git stash push -u -m "tracked and new draft"
git status
git stash list
git stash branch resume-draft "stash@{0}"
git status
git add draft.txt new-draft.txt
git commit -m "Complete resumed draft"
```

The new branch should contain both recovered changes. A successful stash branch removes the applied entry.
