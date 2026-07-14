# Exercise Solutions: Pull, Push, and Collaborate Safely

## Exercise 1

```text
git switch main
git status
git log --graph --oneline --decorate --all
git merge origin/main
git status
git log --graph --oneline --decorate --all
```

Bob's `main` should move to the fetched Alice commit, and `team.txt` should appear.

## Exercise 2

```text
git switch -c bob-note
git add bob.txt
git commit -m "Add Bob's team note"
git push -u origin bob-note
git branch -vv
git branch --remotes
git switch main
```

Create `bob.txt` before staging. The verbose list should show `bob-note` tracking `origin/bob-note`.

## Exercise 3

In Alice:

```text
git switch main
git add team.txt
git commit -m "Add Alice team update"
git push origin main
```

In Bob, after independently editing and committing:

```text
git add team.txt
git commit -m "Add Bob team update"
git push origin main
git fetch origin
git log --oneline main..origin/main
git log --oneline origin/main..main
git merge origin/main
git status
git push origin main
git rev-list --left-right --count main...origin/main
```

The first push should be rejected. If both contributors appended nearby lines, resolve the conflict by keeping both updates, stage, and commit the merge. The final count should be `0 0`.
