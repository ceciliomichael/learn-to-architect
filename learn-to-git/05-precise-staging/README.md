# Module 05: Stage the Exact Changes You Want

## What you will learn

You will stage selected files and selected parts of a file, correct the index, and record file moves and removals.

## Stage by path

The safest everyday form names the intended paths:

```text
git add README.md notes.txt
```

`git add .` stages changes under the current folder, including new files and deletions. It is convenient, but inspect first because its selection can be wider than intended.

## Stage part of a file

One file can contain two unrelated edits. Review and select hunks interactively:

```text
git add -p notes.txt
```

Git displays a hunk and asks what to do. The most useful responses are:

- `y`: stage this hunk
- `n`: do not stage this hunk
- `s`: split the hunk into smaller hunks when possible
- `q`: stop and leave remaining hunks unstaged
- `?`: show help

Afterward, inspect both versions:

```text
git diff
git diff --staged
```

Interactive staging does not change your working file. It changes what is copied into the index.

## Correct the staging area

If you staged a file by mistake, copy its `HEAD` version back into the index while keeping the working edit:

```text
git restore --staged unwanted.txt
```

This unstages the path. It does not discard the working tree edit. Always confirm with status and both diff views.

For a newly added file, the command removes it from the index and leaves it as an untracked working file.

## Stage a deletion or rename

Remove a tracked file and stage that removal:

```text
git rm old-notes.txt
```

Rename or move a tracked file and stage the result:

```text
git mv notes.txt guide.txt
```

Git ultimately records snapshots, not a permanent rename event. During comparison, it can recognize similar deleted and added content as a rename.

You can also move a file with normal file tools and then stage the old and new paths. `git mv` is a convenient shortcut.

## Build focused commits

For each intended purpose:

1. Inspect all changes.
2. Stage the related paths or hunks.
3. Inspect the staged diff.
4. Commit with a message describing that purpose.
5. Repeat for the remaining changes.

## Common mistakes

### Using `git add .` without checking location

Its scope begins at the current folder. Use `git status --short` and name paths when precision matters.

### Using restore without `--staged`

`git restore path` affects the working tree and can discard an edit. In this lesson, use the explicit `--staged` form to correct only the index.

### Assuming Git permanently tracks renames

Git stores before and after snapshots. Rename detection happens when Git compares them.

## Check your understanding

You are ready when you can stage one path, stage one hunk, and unstage without losing the working edit.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
