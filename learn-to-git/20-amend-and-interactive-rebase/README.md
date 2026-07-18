# Module 20: Amend and Clean Private History

## What you will learn

You will replace the latest private commit and use interactive rebase to reorder, combine, rename, edit, or remove private commits.

## Amend the latest commit

If the most recent local commit has a missing file or poor message, make the correction, stage it, and run:

```text
git commit --amend
```

Git creates a replacement commit using the staged snapshot and opens the message for editing. Even if only the message changes, the new commit has a different hash.

Keep the current message while adding staged content:

```text
git commit --amend --no-edit
```

Amend only commits you are allowed to rewrite. For a published shared commit, add a new correction commit instead.

## Plan an interactive rebase

To edit the latest three private commits:

```text
git branch backup-before-cleanup
git rebase -i HEAD~3
```

Git opens a todo list from oldest selected commit to newest. Each line starts with an action.

Useful actions include:

- `pick`: keep the commit
- `reword`: keep its patch but edit its message
- `edit`: pause after applying it so you can amend it
- `squash`: combine it with the previous selected commit and edit messages
- `fixup`: combine it with the previous selected commit while normally discarding this commit's message
- `drop`: remove the commit

You can reorder lines to reorder commits. Reordering may conflict or change behavior, so test the result.

## Edit a chosen commit

When rebase pauses at an `edit` line:

```text
git status
```

Make and stage corrections, then replace that commit:

```text
git commit --amend
git rebase --continue
```

If the original commit should remain unchanged, simply continue.

## Abort and verify

Before completion, abort returns to the old branch state:

```text
git rebase --abort
```

After completion:

```text
git log --graph --oneline --decorate --all
git diff backup-before-cleanup..HEAD
```

An empty diff means the final project snapshot matches the backup, even though commit organization changed. Run the project's tests too.

## Common mistakes

### Squashing into the following line

Squash and fixup combine a commit into the previous selected line, not the next one.

### Deleting a todo line accidentally

Removing a line means dropping that commit in modern Git. Use `drop` when intentional because it states your purpose clearly.

### Cleaning history after teammates use it

Interactive rebase replaces selected commits. Keep it to private history or coordinate explicitly.

## Check your understanding

You are ready when you can amend the latest commit, read the oldest-to-newest todo list, and verify the final snapshot after a cleanup.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
