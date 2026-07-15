# Exercise Solutions: Fetch and Remote-Tracking Branches

## Exercise 1

In Alice, after creating the file:

```text
git add team.txt
git commit -m "Add shared team note"
git push origin main
```

Bob is an independent repository. Its `origin/main` does not change until Bob communicates with the remote.

## Exercise 2

```text
cd ../bob
git log --graph --oneline --decorate --all
git fetch origin
git log --graph --oneline --decorate --all
git log --oneline main..origin/main
```

The graph should show `origin/main` one commit ahead of `main`. Fetch does not check out `team.txt`, so it remains absent from the working tree.

## Exercise 3

```text
git branch -vv
git rev-list --left-right --count main...origin/main
git show origin/main:team.txt
```

The count should normally be `0 1`. Git downloaded the commit and file objects, so it can read their snapshot without moving `main` or changing the working tree.
