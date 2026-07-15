# Exercise Solutions: Reflog, Detached HEAD, and Recovery

## Exercise 1

```text
git log --graph --oneline --decorate --all
git reflog
git show RECOVERED_HASH
git branch reflog-recovery RECOVERED_HASH
git log --graph --oneline --decorate --all
```

Choose a hash that points to the wanted later commit. Your reflog selectors and hashes will differ.

## Exercise 2

Find the oldest hash with `git log --reverse --oneline`, then:

```text
git switch --detach OLDEST_HASH
git branch --show-current
git status
git add experiment.txt
git commit -m "Try detached experiment"
git log --graph --oneline --decorate --all
git reflog -5
```

Create the experiment file before staging. An empty result from `git branch --show-current` confirms detached state.

## Exercise 3

```text
git switch -c saved-experiment
git branch --show-current
git switch main
git log --oneline saved-experiment
git branch --contains saved-experiment
```

The new branch now gives the experiment commit a lasting reachable name.
