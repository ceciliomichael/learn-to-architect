# Exercise Solutions: Maintain Large and Long-Lived Repositories

## Exercise 1

```text
git count-objects -vH
git rev-parse --git-path objects/pack
git fsck
```

A healthy repository may still report dangling objects after earlier history edits. Record the exact output rather than deleting anything.

## Exercise 2

From the parent folder, a bare backup can be created with:

```text
git clone --bare disposable-repository disposable-backup.git
```

Back in the practice repository:

```text
git gc
git count-objects -vH
git fsck
```

Git may pack loose objects. A tiny repository may show little useful size reduction, which is expected.

## Exercise 3

Useful inspection commands include:

```text
git status --short
git ls-files
git log --stat -5
git diff --staged --stat
```

Your note should name project source and required small assets as Git content, reproducible output as ignored content, release archives as artifact content, and unusually large versioned assets as a policy decision.
