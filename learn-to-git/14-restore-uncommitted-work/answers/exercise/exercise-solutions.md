# Exercise Solutions: Restore Uncommitted Work

## Setup

```text
mkdir restore-practice
cd restore-practice
git init
git add notes.txt
git commit -m "Add saved note"
```

Create the stated file content with an editor before staging.

## Exercise 1

After adding and staging the draft line:

```text
git diff --staged
git restore --staged notes.txt
git status
git diff
```

The edit should move from the staged comparison to the unstaged comparison.

## Exercise 2

After making an outside copy:

```text
git restore notes.txt
git status
```

Status should be clean. Open the file and confirm its committed content.

## Exercise 3

```text
git clean -n
git clean -nd
git status --short
```

The first preview should name the loose file. The second should also name the untracked directory. Neither command removes them.
