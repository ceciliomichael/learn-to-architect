# Exercise Solutions: Branches, HEAD, and Switching

## Exercise 1

```text
mkdir branch-practice
cd branch-practice
git init
git add story.txt
git commit -m "Start story"
git branch --show-current
```

Create `story.txt` in your editor before staging it. The final output should be `main`.

## Exercise 2

```text
git switch -c add-middle
git add story.txt
git commit -m "Add middle to story"
git log --graph --oneline --decorate --all
git switch main
```

After the topic commit, `HEAD` and `add-middle` point to it. `main` points to its parent. Switching to `main` loads the older snapshot, which has no middle line.

## Exercise 3

```text
git branch
git log --graph --oneline --decorate --all
git switch add-middle
git branch -m story-middle
git branch
git status
```
