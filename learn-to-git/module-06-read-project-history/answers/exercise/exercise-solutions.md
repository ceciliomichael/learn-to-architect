# Exercise Solutions: Read Project History

## Exercise 1

```text
git log
git log --oneline --decorate
```

Your hashes and subjects depend on your commits. The newest is first and the oldest is last.

## Exercise 2

Replace `OLDEST_HASH` with the copied value:

```text
git show OLDEST_HASH
git show --stat OLDEST_HASH
git log -2 --oneline
```

The first line of the two-entry log is `HEAD`; the next is normally `HEAD^`. The current commit records the parent hash, linking the two.

## Exercise 3

Use the current path of your notes file:

```text
git log --follow -- first.txt
git log --oneline --grep="diff"
git log --graph --oneline --decorate --all
```

Choose a different search word if your messages do not contain `diff`.
