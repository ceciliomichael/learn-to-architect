# Module 02: Repositories and Git's Three Locations

## What you will learn

You will create a repository and understand the working tree, staging area, and committed history.

## Create a repository

Enter your course practice folder, create a project, and initialize Git:

```text
mkdir three-locations
cd three-locations
git init
```

`git init` creates Git's private data inside a hidden `.git` folder. The project folder is now a repository. Do not manually edit `.git` while learning.

Run:

```text
git status
```

Status is your main orientation command. It reports the current branch and the state of files.

## The three locations

A file can be represented in three important places.

### 1. Working tree

The working tree is the files you can see and edit in the project folder. Saving a file changes the working tree.

### 2. Staging area

The staging area holds the exact content planned for the next commit. Git also calls it the index.

`git add` copies current file content from the working tree into the staging area:

```text
git add notes.txt
```

Staging does not save a permanent version. It prepares one.

### 3. Committed history

A commit records the staged snapshot, its author information, a message, and a connection to its parent commit. Commits form repository history.

You will create commits in the next module. For now, focus on the movement:

```text
working tree -> git add -> staging area -> git commit -> history
```

## Tracked and untracked files

Create `notes.txt` in your editor with this content:

```text
Git records project history.
```

Run `git status`. The file is untracked because the repository has not started following it.

Stage it:

```text
git add notes.txt
git status
```

The file is now tracked and staged. Git has stored its current content in the index.

## Staging is a copy, not a label

After staging `notes.txt`, add another line in your editor:

```text
The working tree can change again.
```

Now `git status` shows the same file under both staged changes and unstaged changes. This is possible because the index holds the first version while the working tree holds the newer version.

Run `git add notes.txt` again to update the staged copy. Status will then show only the staged change.

## Repository boundaries

Git commands normally apply to the repository containing your current folder. Before doing important work, run:

```text
git rev-parse --show-toplevel
```

It prints the repository's root folder. Outside a repository, most Git project commands report an error.

## Common mistakes

### Thinking `git add` means add once

You run `git add` whenever you want to copy the current content into the staging area, even for already tracked files.

### Thinking staging stores the whole working tree automatically

Only content selected by an add command enters the index.

### Initializing the wrong folder

Use `pwd` before `git init`. Use `git rev-parse --show-toplevel` afterward.

## Check your understanding

You are ready when you can explain which command moves content into the staging area and why one file can have both staged and unstaged changes.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
