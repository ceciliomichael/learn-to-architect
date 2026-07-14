# Exercise Solutions: Rebase a Private Branch

## Exercise 1

```text
mkdir rebase-practice
cd rebase-practice
git init
git add base.txt
git commit -m "Add base file"
git switch -c topic
git add topic-one.txt
git commit -m "Add first topic file"
git add topic-two.txt
git commit -m "Add second topic file"
git switch main
git add main-update.txt
git commit -m "Add main update"
git log --graph --oneline --decorate --all
```

Create each file before its add command.

## Exercise 2

```text
git switch topic
git status
git branch topic-before-rebase
git rebase main
git log --graph --oneline --decorate --all
```

The original topic hashes remain reachable from the safety branch. The current topic has new hashes based on the main update.

## Exercise 3

```text
git switch main
git merge topic
git log --graph --oneline --decorate --all
git branch -d topic
```

Because rebased topic starts at the former main tip, main can move forward without a merge commit.
