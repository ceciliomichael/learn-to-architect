# Exercise Solutions: Create Your First Commits

## Exercise 1

```text
git status
git commit -m "Add first Git notes"
git status
git show --stat --oneline HEAD
```

After the commit, status should be clean unless you made another edit.

## Exercise 2

After editing `notes.txt` and creating `later.txt`:

```text
git add notes.txt
git status
git commit -m "Explain focused commits"
git status
```

Before the commit, `notes.txt` should be staged and `later.txt` should be untracked. Afterward, `later.txt` should remain untracked. Confirm the committed file list:

```text
git show --name-only --format=short HEAD
```

It should name `notes.txt`, not `later.txt`.

## Exercise 3

After replacing the text:

```text
git add later.txt
git status
git commit -m "Add commit review reminder"
git show --stat --oneline HEAD
```

Your message may differ, but it should describe the purpose clearly.
