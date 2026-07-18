# Module 22: Mark Releases with Tags

## What you will learn

You will create annotated and lightweight tags, inspect them, publish them deliberately, and correct a mistaken local tag.

## A tag names a chosen object

Branches usually move as new commits are created. Tags normally stay on the chosen object. Projects use them to name releases and other important points.

List tags:

```text
git tag
git tag --list "v1.*"
```

## Annotated tags

Create an annotated tag at `HEAD`:

```text
git tag -a v1.0.0 -m "Release version 1.0.0"
```

An annotated tag is a tag object with a name, tagger, date, message, and target. It can also be cryptographically signed when signing is configured. Annotated tags are a useful default for releases.

Tag a specific commit:

```text
git tag -a v0.9.0 COMMIT -m "Release version 0.9.0"
```

## Lightweight tags

```text
git tag test-point
```

A lightweight tag is a reference directly to an object, without a separate tag message and tagger object. It can suit temporary or private markers.

## Inspect tags

```text
git show v1.0.0
git show-ref --tags
git log --oneline --decorate
```

`git show` displays annotated tag information and the tagged object. The decorated log shows names at their commit positions.

## Tags are not pushed automatically by a normal branch push

Publish one tag deliberately:

```text
git push origin v1.0.0
```

`git push --tags` publishes all tags missing from the remote. This can send private or accidental tags, so listing and pushing one release tag is clearer.

## Correct a mistaken tag

Delete a local tag:

```text
git tag -d mistaken-tag
```

Delete a remote tag only after coordination:

```text
git push origin --delete mistaken-tag
```

Moving an already published release tag is confusing because other clones may retain the old target. Prefer a corrected new version tag unless project policy says otherwise.

## Version names

Git does not impose a version scheme. A common project convention uses names such as `v2.3.1`, but the project's documented release policy decides the meaning.

## Common mistakes

### Tagging the wrong commit

Inspect `git show COMMIT` before creating the tag, then inspect the tag afterward.

### Assuming tags move with the branch

They normally remain at their original targets.

### Publishing every local tag

Push the intended tag by name.

## Check your understanding

You are ready when you can create and verify an annotated release tag and explain why publishing it is a separate action.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
