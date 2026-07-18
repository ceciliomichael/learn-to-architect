# Module 11: Clone Repositories and Understand Remotes

## What you will learn

You will clone a repository, inspect the remote named `origin`, and create a safe local collaboration lab.

## Local and remote repositories

A remote is another Git repository that your repository knows by a short name and a location. The other repository may be on the same computer, on a network server, or on a hosting service.

A remote is not a live shared folder. Your working repository has its own objects, branches, index, and working tree. You exchange commits deliberately.

## Clone an existing repository

```text
git clone PATH_OR_URL project-copy
```

Clone normally:

1. Creates `project-copy`.
2. Copies the reachable repository data.
3. Adds the source location as a remote named `origin`.
4. Creates and checks out an initial local branch based on the source repository's default branch.

`origin` is only a conventional name. Git does not give it special authority.

## Inspect remotes

```text
git remote
git remote -v
git remote show origin
```

`-v` shows the locations used for fetching and pushing. They are often the same but can differ.

## Add, rename, or change a remote

For a repository you initialized yourself:

```text
git remote add origin PATH_OR_URL
```

Rename a remote:

```text
git remote rename origin upstream
```

Change its location:

```text
git remote set-url origin NEW_PATH_OR_URL
```

These commands change local configuration. They do not move the remote repository.

## A bare repository for safe practice

A normal repository has a working tree. A bare repository has Git data but no checked-out project files. Servers commonly use bare repositories as exchange points.

Create a bare copy of an existing clean repository:

```text
git clone --bare branch-practice shared-project.git
```

The `.git` suffix is a convention for bare repository folders.

Then make two independent working clones:

```text
git clone shared-project.git alice
git clone shared-project.git bob
```

This lab lets you practice two contributors on one computer without internet access.

## Verify where you are

A collaboration lab contains similar folders. In every shell, check:

```text
pwd
git rev-parse --show-toplevel
git remote -v
git status
```

## Common mistakes

### Editing the bare repository

A bare repository has no working tree. Make normal clones for editing.

### Assuming clone links working files live

Clones exchange Git data only when you fetch, pull, or push.

### Running a command in Alice when you mean Bob

Print the path and repository root before each collaboration step.

## Check your understanding

You are ready when you can explain what clone creates, what `origin` stores, and why the course uses a bare local remote.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
