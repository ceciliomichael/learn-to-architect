# Module 03: Create Your First Commits

## What you will learn

You will commit a staged snapshot, write useful commit messages, and verify what a commit contains.

## Before you begin

Use the `three-locations` repository from Module 02. Run `git status`. `notes.txt` should be staged.

If it is not staged, run:

```text
git add notes.txt
```

## Create the commit

Run:

```text
git commit -m "Add introductory Git notes"
```

Git creates a commit from the staging area, not from every current file automatically. The `-m` option supplies its message.

Run:

```text
git status
```

A clean working tree means the working tree and staging area match the current commit. It does not mean the repository has no files or history.

## What a commit records

A commit includes:

- A snapshot of staged project content
- The author's name, email, and time
- The committer's name, email, and time
- A message
- A link to its parent commit, except for the first commit

Git identifies the commit with a hash. A short hash may look like `a1b2c3d`, but your value will differ.

Inspect the newest commit:

```text
git show --stat --oneline HEAD
```

`HEAD` means the commit currently checked out through the current branch.

## Make one understandable change

Add this line to `notes.txt`:

```text
A commit records staged content.
```

Then use the reliable commit loop:

```text
git status
git add notes.txt
git status
git commit -m "Explain what a commit records"
git status
```

The second status check is deliberate. It gives you a final chance to confirm what will be committed.

## Write useful messages

A short commit subject should say what the commit accomplishes. Use a direct action phrase:

```text
Add setup instructions
Fix total calculation
Remove outdated contact details
```

Avoid messages such as `changes`, `stuff`, or `work`. They do not help a future reader understand the history.

A good commit usually represents one coherent purpose. If two unrelated changes can be explained separately, stage and commit them separately.

## Nothing to commit

If the staging area matches `HEAD`, `git commit` reports that there is nothing to commit. This is information, not damage. Inspect status, edit a file, and stage the intended content.

## Common mistakes

### Assuming commit includes every saved edit

Commit uses the index. An unstaged edit stays outside the new commit.

### Staging without inspecting status

A commit can accidentally include extra files. Inspect before and after staging.

### Treating a commit as a cloud backup

A local commit is stored in this local repository. Remote copies are taught later.

## Check your understanding

You are ready when you can describe where commit content comes from, create a focused commit, and inspect it with `git show`.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
