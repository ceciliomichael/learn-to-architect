# Plan for the Git Learning Module V2

## Purpose

This document tracks the design and implementation of `git-learning-module-v2/`.

The course is for a learner who has never used version control or a command-line tool. It begins with a disposable practice repository and grows toward safe collaboration, recovery, history editing, repository investigation, and advanced Git features.

## Findings from the original Git course

The original course contains useful commands, but four modules are not enough for a careful beginner-to-advanced path.

The main problems found during review are:

1. The first module introduces initialization, status, staging, commits, history, and several pitfalls at once.
2. The mental model depends heavily on long analogies instead of showing the exact working tree, index, commit, reference, and remote-tracking relationships.
3. Diff inspection and precise staging are not taught before learners are asked to commit.
4. Branch creation and merge conflicts arrive before learners have studied commit graphs and `HEAD`.
5. Remote collaboration combines remotes, push, fetch, pull, and clone without first separating remote-tracking branches from local branches.
6. Recovery introduces detached `HEAD`, revert, all reset modes, and reflog together.
7. Destructive commands are described dramatically but not placed inside a consistent safety procedure.
8. Important everyday topics are missing, including `.gitignore`, `git restore`, partial staging, upstream branches, stashing, rebase, tags, cherry-pick, worktrees, bisect, hooks, and repository internals.
9. Exercises sometimes assume a hosted remote. V2 will use local repositories first so every learner can practice without an account or network connection.
10. Some statements overpromise Git as unbreakable or seamless. Git protects recorded objects well, but uncommitted work, force updates, expiration, and external hosting still require care.

## Course promise

A learner who completes V2 should be able to:

- create and inspect a repository without guessing about its current state
- make focused commits that contain exactly the intended changes
- read diffs and history before changing anything
- create, switch, compare, merge, and remove branches safely
- resolve conflicts while understanding which versions are involved
- clone, fetch, pull, and push with a correct local and remote mental model
- choose between restore, revert, reset, and reflog based on what must change
- recover commits and uncommitted arrangements when Git still has the necessary data
- rebase private work and avoid rewriting shared history casually
- use stashes, tags, cherry-picks, and worktrees for practical workflows
- investigate regressions with log, blame, and bisect
- understand commits, trees, blobs, refs, `HEAD`, and the object database
- use hooks, submodules, and maintenance features with their real tradeoffs

## Writing rules

Every V2 file must:

1. Use no emoji.
2. Use no em dash character.
3. Prefer direct explanations over dramatic analogies.
4. Define every Git term before relying on it.
5. Separate observation commands from commands that change state.
6. Explain which locations a command can change: working tree, index, current branch, other refs, or remote.
7. Never describe a destructive command without a safe practice setup and recovery discussion.
8. Use `git switch` and `git restore` for their focused purposes while still teaching how older `git checkout` examples map to them.
9. Use `main` as the course default branch while explaining that repositories can use other names.
10. Never assume a GitHub, GitLab, or other hosting account.
11. Use local bare repositories to teach remote behavior before hosted collaboration.
12. Avoid commands that change the real course repository in exercises.
13. Mark placeholder values clearly, such as `<branch>` or `<commit>`.
14. Explain output that varies by Git version or operating system.
15. Present workflow preferences as choices, not Git laws.

## Required module structure

Every module will contain:

```text
module/
|-- README.md
|-- exercise/
|   `-- exercise.md
|-- quiz/
|   `-- quiz.md
`-- answers/
    |-- exercise/
    |   `-- exercise-solutions.md
    `-- quiz/
        `-- quiz-answers.md
```

Lessons will include:

- `Before you start`
- `What you will learn`
- `Why this matters`
- focused explanations and command examples
- `Safety check` where a command can discard or rewrite data
- `Common mistakes`
- `Check your understanding`
- links to exercises and quiz
- the next module

Exercises will run in disposable repositories created for the course. Answers will include commands, expected state, and verification commands.

## Curriculum roadmap

### Part 1: Safe local foundations

- [x] **Module 01: Install Git and Create a Safe Practice Space**
  - Teaches version checks, identity configuration, help, terminal location, and the disposable practice rule

- [x] **Module 02: Repositories and Git's Three Main Locations**
  - Teaches repository, working tree, index, current commit, `.git`, tracked and untracked files

- [x] **Module 03: Create Your First Commits**
  - Teaches `init`, `status`, `add`, `commit`, focused messages, and clean-state verification

- [x] **Module 04: Read Changes with Diff**
  - Teaches unstaged diff, staged diff, word diff, summary views, and why status is not enough

- [x] **Module 05: Stage Changes Precisely**
  - Teaches file staging, partial staging with `add -p`, moving changes between working tree and index, and commit boundaries

- [x] **Module 06: Read Commit History**
  - Teaches `log`, `show`, commit ids, relative revisions, graph views, and path-limited history

- [x] **Module 07: Ignore Files and Manage Tracked Content**
  - Teaches `.gitignore`, patterns, negation, repository-local excludes, global ignores, and why ignore does not untrack files

### Part 2: Branches and integration

- [x] **Module 08: Branches, HEAD, and Switching**
  - Teaches branch pointers, `HEAD`, `branch`, `switch`, creation, renaming, and safe deletion checks

- [x] **Module 09: Merge Branches**
  - Teaches fast-forward and three-way merges, merge commits, `--ff-only`, `--no-ff`, and graph inspection

- [x] **Module 10: Resolve Merge Conflicts**
  - Teaches conflict states, markers, ours and theirs in merge context, resolution, abort, and verification

### Part 3: Remotes and collaboration

- [x] **Module 11: Clone and Configure Remotes**
  - Teaches bare repositories, clone, origin, remote urls, refs, and offline remote practice

- [x] **Module 12: Fetch and Tracking Branches**
  - Teaches fetch, remote-tracking branches, upstream configuration, ahead and behind, and comparison before integration

- [x] **Module 13: Pull, Push, and Team Collaboration**
  - Teaches pull as fetch plus integration, merge versus rebase policies, push, upstreams, rejected pushes, feature branches, forks, and review requests

### Part 4: Undo and recovery

- [x] **Module 14: Restore Uncommitted Work Safely**
  - Teaches restore working files, restore staged files, previewing `clean`, and protecting untracked data

- [x] **Module 15: Revert Published Changes**
  - Teaches inverse commits, reverting ranges and merge commits carefully, and shared-history safety

- [x] **Module 16: Reset Local History**
  - Teaches soft, mixed, and hard reset by exact location changes, path reset, backup refs, and private-history limits

- [x] **Module 17: Reflog, Detached HEAD, and Recovery**
  - Teaches local reference logs, detached inspection, naming valuable commits, recovering moved or deleted branch tips, and expiration limits

### Part 5: Reshaping and moving work

- [x] **Module 18: Stash Temporary Work**
  - Teaches stash push, list, show, apply, pop, drop, untracked inclusion, and conflict handling

- [x] **Module 19: Rebase Private Branches**
  - Teaches replay, conflict continuation and abort, merge comparison, pull rebase, and the shared-history warning

- [x] **Module 20: Amend and Interactive Rebase**
  - Teaches amend, reword, reorder, squash, fixup, edit, autosquash concepts, and safe history-edit boundaries

- [x] **Module 21: Cherry-Pick Focused Commits**
  - Teaches applying selected commits, conflicts, abort, duplicate-change risks, and when merge is better

- [x] **Module 22: Tags and Release Points**
  - Teaches lightweight and annotated tags, tag inspection, pushing tags, signed tag concepts, and immutable release naming practices

- [x] **Module 23: Work with Multiple Working Trees**
  - Teaches `git worktree`, linked branch safety, list, add, remove, prune, and practical parallel work

### Part 6: Investigation and advanced repository knowledge

- [x] **Module 24: Investigate History with Log, Blame, and Bisect**
  - Teaches search filters, pickaxe, line history limits, blame interpretation, manual and automated bisect, and investigation notes

- [x] **Module 25: Git Objects, Trees, Commits, and References**
  - Teaches content-addressed objects, blobs, trees, commits, refs, symbolic `HEAD`, reachability, and safe plumbing inspection

- [x] **Module 26: Configuration, Aliases, and Attributes**
  - Teaches configuration scopes, inspection origin, safe aliases, `.gitattributes`, line endings, diff drivers, and precedence

- [x] **Module 27: Hooks and Local Automation**
  - Teaches client and server hook concepts, executable scripts, bypass limits, security, shared hook tools, and CI as the enforceable boundary

- [x] **Module 28: Submodules and Nested Repositories**
  - Teaches gitlinks, clone initialization, update, recorded commits, detached submodule state, publishing order, and alternatives

- [x] **Module 29: Repository Maintenance and Large Histories**
  - Teaches `gc`, maintenance, integrity checks, pruning cautions, shallow and partial clones, sparse checkout, large-file strategies, and backup boundaries

## Dependency rules

- Status and the three locations must be understood before undo commands.
- Diff inspection must come before partial staging and committing workflows.
- Commit graphs and `HEAD` must come before merge, rebase, and reset.
- Local branches must come before remote-tracking branches.
- Fetch must be understood before pull.
- Restore must be taught before reset.
- Revert must be taught before history-rewriting reset and rebase.
- Reflog must be taught before interactive history editing.
- Merge conflicts must be taught before rebase and cherry-pick conflicts.
- Ordinary repositories must be understood before submodules and worktrees.
- Porcelain commands must be familiar before object-database plumbing.

## Safety protocol for exercises

Every exercise that changes history or discards work will require:

1. Confirm the terminal path with `pwd` or the platform equivalent.
2. Confirm the repository root with `git rev-parse --show-toplevel`.
3. Confirm state with `git status --short --branch`.
4. Use a repository created specifically for the exercise.
5. Create a temporary backup branch or tag when the lesson requires recovery practice.
6. Inspect the target commit before changing a reference.
7. Run the change.
8. Verify the working tree, index, refs, and log afterward.

No course exercise will run a destructive command against this learning repository.

## Accuracy rules

- `git fetch` downloads objects and updates configured remote-tracking refs. It does not integrate them into the current local branch by itself.
- `git pull` fetches and then integrates according to arguments and configuration.
- `git restore` changes working-tree and optionally index content. It does not move the current branch.
- `git reset` can move the current branch and can also change the index and working tree depending on mode.
- `git revert` records a new commit that applies the inverse of selected changes.
- Reflogs are local, reference-specific records and are not permanent backups.
- Branches and tags are names pointing to objects, not independent copies of files.
- A force push can overwrite a remote reference and must use an explicit team policy. `--force-with-lease` reduces some risk but is not a universal guarantee.
- Git usually stores complete content objects, while display tools describe differences between snapshots.
- Hooks are local by default and are not automatically installed for every clone.
- Submodules record a commit from another repository, not the nested repository's current branch intention.

## Estimated learning time

- Modules 01 to 07: 18 to 28 hours
- Modules 08 to 13: 18 to 30 hours
- Modules 14 to 17: 14 to 24 hours
- Modules 18 to 23: 18 to 30 hours
- Modules 24 to 29: 22 to 36 hours

The complete course is expected to take roughly 90 to 148 focused hours.

## Implementation checklist

- [x] Audit the original Git course
- [x] Define the V2 module sequence and safety rules
- [x] Create the Git V2 root guide
- [x] Create Modules 01 to 07
- [x] Create Modules 08 to 13
- [x] Create Modules 14 to 17
- [x] Create Modules 18 to 23
- [x] Create Modules 24 to 29
- [x] Verify required folder structure
- [x] Check relative Markdown links
- [x] Scan for emoji, em dash characters, placeholders, and unbalanced code blocks
- [x] Run command workflows in disposable local repositories
- [x] Update the repository root README
- [x] Mark all roadmap items complete

## Definition of done

Git V2 is complete when:

1. All 29 modules contain the lesson, exercise, quiz, and both answer files.
2. Every exercise uses a disposable practice repository.
3. Risky commands include scope, safety, and verification guidance.
4. Quiz questions use only the current and earlier modules.
5. All internal links resolve.
6. V2 contains no emoji or em dash characters.
7. Tested command sequences produce the described repository states on the current Git version.
8. No miscellaneous or final assessment folder is added.
9. The root README recommends Git V2 while retaining the original course for reference.
