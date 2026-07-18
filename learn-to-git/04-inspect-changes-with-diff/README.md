# Module 04: Inspect Changes with Diff

## What you will learn

You will inspect unstaged changes, staged changes, and the content of a commit before trusting your next action.

## Why diff comes before more commands

`git status` names changed files. A diff shows the changed lines. Use both: status for orientation, diff for evidence.

## Inspect unstaged changes

Add a line to a tracked file but do not stage it. Run:

```text
git diff
```

With no extra arguments, `git diff` compares the working tree with the staging area. Lines beginning with `-` are from the old side. Lines beginning with `+` are from the new side. The marker lines `---` and `+++` name the compared files and are not deleted or added project text.

A block of nearby changes is called a hunk. Its header begins with `@@` and includes line locations.

## Inspect staged changes

After staging the file, plain `git diff` becomes empty if no further edits exist. The change moved into the index. Compare the index with `HEAD`:

```text
git diff --staged
```

`--cached` is another spelling of `--staged`.

Use this sequence before every commit:

```text
git status
git diff
git diff --staged
```

## Compare commits

`HEAD` names the current commit. `HEAD^` usually names its first parent. After you have at least two commits:

```text
git diff HEAD^ HEAD
```

You can also compare two commit hashes:

```text
git diff abc1234 def5678
```

Replace the examples with hashes from your repository.

## Limit the view

Show changes for one path:

```text
git diff -- notes.txt
git diff --staged -- notes.txt
```

The separate `--` tells Git that what follows is a path, not an option or revision.

For small word-level edits, this view can help:

```text
git diff --word-diff
```

## Diff does not change files

The commands in this lesson inspect. They do not stage, commit, restore, or delete content. When uncertain, inspection is a safe first step.

## Common mistakes

### Plain diff looks empty after staging

Use `git diff --staged`. Plain diff only shows working tree content not already in the index.

### Reading every minus sign as a deleted file

Inside a hunk, minus and plus identify old and new lines. File deletion is described separately in the diff header.

### Committing from status alone

Status cannot show whether an unintended line is staged. Read the staged diff.

## Check your understanding

You are ready when you can choose the correct diff for unstaged and staged changes and explain what its plus and minus lines mean.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
