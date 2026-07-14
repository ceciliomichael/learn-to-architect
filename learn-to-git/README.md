# Git Learning Module V2

This course teaches Git from the beginning. You do not need programming experience or command-line experience.

Git records useful versions of a project. It also helps people work together, inspect changes, and recover from mistakes. This course teaches those skills in a safe order. Early exercises use disposable folders, and remote exercises use a local practice remote, so you can learn without risking a real project.

## How to use this course

Complete the modules in order. Each module contains:

1. A lesson in `README.md`
2. Guided work in `exercise/exercise.md`
3. A short knowledge check in `quiz/quiz.md`
4. Worked exercise solutions in `answers/exercise/exercise-solutions.md`
5. Explained quiz answers in `answers/quiz/quiz-answers.md`

Type every command yourself. Read Git's output before continuing. When your result differs from the lesson, use `git status` first.

## What you need

You need Git 2.23 or newer because this course uses `git switch` and `git restore`. A current Git release is recommended. You also need a terminal and a plain text editor.

All commands work in Git Bash. Most also work in PowerShell and macOS or Linux terminals. File creation commands differ between shells, so the exercises tell you when to use your editor.

## Course path

### Part 1: Build a reliable foundation

- [Module 01: Install Git and Create a Safe Practice Area](module-01-install-git-and-safe-practice/README.md)
- [Module 02: Repositories and Git's Three Locations](module-02-repositories-and-three-locations/README.md)
- [Module 03: Create Your First Commits](module-03-first-commits/README.md)
- [Module 04: Inspect Changes with Diff](module-04-inspect-changes-with-diff/README.md)
- [Module 05: Stage the Exact Changes You Want](module-05-precise-staging/README.md)
- [Module 06: Read Project History](module-06-read-project-history/README.md)
- [Module 07: Ignore Generated and Private Files](module-07-ignore-files/README.md)

### Part 2: Work with branches

- [Module 08: Branches, HEAD, and Switching](module-08-branches-head-and-switching/README.md)
- [Module 09: Combine Work with Merge](module-09-combine-work-with-merge/README.md)
- [Module 10: Resolve Merge Conflicts](module-10-resolve-merge-conflicts/README.md)

### Part 3: Work with remotes and other people

- [Module 11: Clone Repositories and Understand Remotes](module-11-clone-and-remotes/README.md)
- [Module 12: Fetch and Remote-Tracking Branches](module-12-fetch-and-tracking/README.md)
- [Module 13: Pull, Push, and Collaborate Safely](module-13-pull-push-and-collaboration/README.md)

### Part 4: Undo and recover safely

- [Module 14: Restore Uncommitted Work](module-14-restore-uncommitted-work/README.md)
- [Module 15: Revert Published Commits](module-15-revert-published-commits/README.md)
- [Module 16: Reset Local History](module-16-reset-local-history/README.md)
- [Module 17: Reflog, Detached HEAD, and Recovery](module-17-reflog-and-recovery/README.md)
- [Module 18: Set Work Aside with Stash](module-18-stash/README.md)

### Part 5: Shape and reuse history

- [Module 19: Rebase a Private Branch](module-19-rebase-private-branches/README.md)
- [Module 20: Amend and Clean Private History](module-20-amend-and-interactive-rebase/README.md)
- [Module 21: Copy a Commit with Cherry-Pick](module-21-cherry-pick/README.md)
- [Module 22: Mark Releases with Tags](module-22-tags/README.md)
- [Module 23: Work in Two Branches with Worktrees](module-23-worktrees/README.md)

### Part 6: Investigate and understand Git deeply

- [Module 24: Investigate with Log, Blame, and Bisect](module-24-investigation-tools/README.md)
- [Module 25: Objects, Trees, Commits, and References](module-25-git-internals/README.md)
- [Module 26: Configuration, Aliases, and Attributes](module-26-configuration-and-attributes/README.md)
- [Module 27: Automate Local Checks with Hooks](module-27-hooks/README.md)
- [Module 28: Manage Nested Repositories with Submodules](module-28-submodules/README.md)
- [Module 29: Maintain Large and Long-Lived Repositories](module-29-repository-maintenance/README.md)

## A safety habit for the whole course

Before any command that can discard work or rewrite commits:

1. Run `git status`.
2. Run `git diff` and `git diff --staged`.
3. Decide whether the commits or changes exist anywhere else.
4. Make a temporary branch when you are uncertain: `git branch backup-before-change`.
5. Read the command one more time before pressing Enter.

Speed comes later. Clear inspection comes first.
