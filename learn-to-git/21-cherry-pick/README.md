# Module 21: Copy a Commit with Cherry-Pick

## What you will learn

You will apply one existing commit's change onto another branch and handle a cherry-pick conflict.

## What cherry-pick does

Cherry-pick takes the patch introduced by a selected commit and applies it to the current branch, creating a new commit.

```text
      C  source
     /
A <- B <- D  target
          \
           C'  target after cherry-pick
```

`C'` usually has a different hash because it has a different parent and new committer information. The source commit remains where it was.

## Choose the destination first

```text
git status
git log --graph --oneline --decorate --all
git show SOURCE_COMMIT
git switch target
git cherry-pick SOURCE_COMMIT
```

The current branch receives the new commit. Inspect the source patch and start with a clean working tree.

## Record where a copied change came from

For a public source commit, some teams use:

```text
git cherry-pick -x SOURCE_COMMIT
```

`-x` adds a line to the new commit message naming the original commit. This can help when backporting a fix between release branches.

## Resolve or stop

If the patch conflicts:

```text
git status
```

Edit, stage, and continue:

```text
git add path
git cherry-pick --continue
```

Or abandon the operation:

```text
git cherry-pick --abort
```

`--skip` omits the current selected commit during a multi-commit sequence. Use it only after proving the change is unnecessary or already present.

## When to use another tool

- Use merge to integrate the relationship and complete work of a branch.
- Use rebase to replay a private line of commits onto a new base.
- Use cherry-pick for a specific self-contained change, such as backporting one fix.

Repeated cherry-picking between long-lived branches can duplicate changes and make later merging harder. Follow project policy.

## Common mistakes

### Picking while on the source branch

Switch to the branch that should receive the copy.

### Expecting the same hash

The new parent makes it a new commit.

### Copying a change that depends on earlier commits

Inspect and test dependencies. One patch may not make sense alone.

## Check your understanding

You are ready when you can select a source commit, apply it to the intended destination, and explain why the result is a new commit.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
