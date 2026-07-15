# Exercise Solutions: Combine Work with Merge

## Exercise 1

```text
git switch main
git status
git log --graph --oneline --decorate --all
git merge story-middle
git log --graph --oneline --decorate --all
git branch -d story-middle
```

`main` moves to the topic tip. The branch deletion should succeed because its commit is reachable from `main`.

## Exercise 2

After editing `story.txt`:

```text
git add story.txt
git commit -m "Add story ending"
git switch -c add-title HEAD^
git add title.txt
git commit -m "Add story title"
git log --graph --oneline --decorate --all
```

Create `title.txt` with your editor before staging it.

## Exercise 3

```text
git switch main
git merge add-title
git status
git log --graph --oneline --decorate --all
git show --stat HEAD
git rev-list --parents -n 1 HEAD
```

The final command prints the merge hash followed by two parent hashes.
