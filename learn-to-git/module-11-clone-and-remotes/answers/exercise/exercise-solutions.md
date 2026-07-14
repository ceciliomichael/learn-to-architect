# Exercise Solutions: Clone Repositories and Understand Remotes

## Exercise 1

From `git-course-practice`:

```text
git clone --bare branch-practice shared-project.git
git clone shared-project.git alice
git clone shared-project.git bob
```

You should now have one bare exchange repository and two normal working repositories.

## Exercise 2

```text
cd alice
git rev-parse --show-toplevel
git branch --show-current
git remote -v
git remote show origin
git log --oneline --decorate -5
git status
```

The remote path should lead to `shared-project.git`.

## Exercise 3

Create `alice-only.txt` with an editor, then:

```text
git status --short
cd ../bob
git status --short
```

Bob should be clean and should not contain Alice's untracked file. Return to Alice and delete the untracked file with your operating system's normal file command or file browser.
