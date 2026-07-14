# Exercise Solutions: Investigate with Log, Blame, and Bisect

## Exercise 1

Example commands for a repository containing `settings.txt` are:

```text
git log -S"mode=unsafe" --oneline -- settings.txt
git log -p -S"mode=unsafe" -- settings.txt
git log -G"mode=(safe|unsafe)" --oneline -- settings.txt
```

`-S` considers a change in occurrence count. `-G` considers whether changed patch lines match the expression.

## Exercise 2

```text
git blame tracked-file.txt
git blame -L 1,2 tracked-file.txt
git show COMMIT
git show COMMIT^:tracked-file.txt
```

Replace the path and commit with your evidence. The parent view helps show what existed before.

## Exercise 3

Create and commit each numbered version in your editor. Record hashes with:

```text
git log --reverse --oneline
git bisect start
git bisect bad COMMIT_FIVE
git bisect good COMMIT_ONE
```

For each selected commit, read `state.txt`, then run one of:

```text
git bisect good
git bisect bad
```

Git should identify commit four as the first bad commit. Finish with:

```text
git bisect reset
git branch --show-current
```
