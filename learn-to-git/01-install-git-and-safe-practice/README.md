# Module 01: Install Git and Create a Safe Practice Area

## What you will learn

You will learn what Git does, how to open a terminal, how to check your installation, and how to create a disposable practice folder.

## Before you begin

You do not need to know programming. A project can be a single text file. Git cares about changes to files, not the programming language inside them.

## What Git does

Git is a version control system. It can save named points in a project's history. Each saved point is called a commit.

A commit lets you answer questions such as:

- What changed?
- Who recorded the change?
- When was it recorded?
- What did the project look like at that point?

Git works locally. You can create commits without an internet connection or an account on a hosting site. GitHub, GitLab, and similar services can store Git repositories online, but they are not Git itself.

## Meet the terminal

A terminal is a program where you type commands. It has a current folder, just as a file browser does.

These commands show your current folder:

```text
pwd
```

In PowerShell, `Get-Location` does the same thing. `pwd` also works as a PowerShell shortcut.

These commands list the current folder:

```text
ls
```

These commands enter a folder named `git-practice`:

```text
cd git-practice
```

The exact spelling matters. A space separates parts of a command.

## Check Git

Run:

```text
git --version
```

A successful result begins with `git version`. If the terminal cannot find Git, install it from the official Git website and reopen the terminal.

## Set your commit identity

Commits record an author name and email address. Set them once for your user account:

```text
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Use the identity that you want attached to future commits. Check it with:

```text
git config --global --get user.name
git config --global --get user.email
```

These settings do not sign you into a hosting service.

## Create a safe practice area

Create a folder in a location you understand, then enter it:

```text
mkdir git-course-practice
cd git-course-practice
```

Keep course repositories inside this folder. Do not practice destructive commands in an important project.

## Configure the default starting branch

This course calls the main branch `main`. Set that default for new repositories:

```text
git config --global init.defaultBranch main
```

## Common mistakes

### Confusing Git with GitHub

Git is the local version control tool. GitHub is one service that can host Git repositories.

### Running commands in the wrong folder

Check `pwd` before important work. Later, `git status` will also help confirm which repository you are using.

### Copying the example identity exactly

Replace the sample name and email with your intended identity.

## Check your understanding

You are ready when you can explain why Git works without GitHub, show your current terminal folder, and display your installed Git version.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Next, you will create a repository and see the three places where Git-managed work can exist.
