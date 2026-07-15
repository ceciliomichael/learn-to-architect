# Exercise Solutions: Amend and Clean Private History

## Exercise 1

```text
mkdir history-cleanup
cd history-cleanup
git init
git add guide.txt
git commit -m "Add guide"
git add tip.txt
git commit -m "stuff"
git add tip.txt
git commit --amend -m "Add first usage tip"
git log --oneline
```

Create and edit files before their add commands. The log should show one tip commit with the useful subject.

## Exercise 2

```text
git add part-one.txt
git commit -m "Add lesson draft"
git add part-two.txt
git commit -m "fixup lesson draft"
git add names.txt
git commit -m "Add nmaes"
git branch before-interactive
git log --oneline --decorate -5
```

## Exercise 3

```text
git rebase -i HEAD~3
```

Edit the todo actions to this shape while keeping your actual hashes and subjects:

```text
pick HASH1 Add lesson draft
fixup HASH2 fixup lesson draft
reword HASH3 Add nmaes
```

When prompted for the reword, use `Add names`. Then verify:

```text
git log --oneline --decorate -5
git diff before-interactive..HEAD
```

The diff should be empty because only history organization and messages changed.
