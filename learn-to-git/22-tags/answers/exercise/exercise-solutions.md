# Exercise Solutions: Mark Releases with Tags

## Exercise 1

```text
git branch --show-current
git status
git tag -a v1.0.0 -m "Release version 1.0.0"
git tag practice-point HEAD^
git tag
git show v1.0.0
git show practice-point
git log --graph --oneline --decorate --all
```

The annotated display includes tagger and message. The lightweight display mainly shows its target commit.

## Exercise 2

After creating the file:

```text
git add after-release.txt
git commit -m "Continue after first release"
git log --graph --oneline --decorate --all
git diff v1.0.0..HEAD
```

`main` and `HEAD` identify the new commit. `v1.0.0` remains at the previous one.

## Exercise 3

```text
git tag -d practice-point
git tag
```

Only the selected local tag is deleted.
