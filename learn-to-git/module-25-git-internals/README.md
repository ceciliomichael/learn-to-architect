# Module 25: Objects, Trees, Commits, and References

## What you will learn

You will look beneath normal commands to understand how Git stores content and connects commits, branches, tags, and `HEAD`.

## Content-addressed storage

Git stores objects under names calculated from their type and content. If the relevant content changes, the object identifier changes. Repositories traditionally use SHA-1 object names, while Git also supports repositories using SHA-256. Scripts should not assume every full object name always has 40 characters.

Normal porcelain commands such as add and commit manage this safely. The inspection commands in this module are often called plumbing commands.

## The four object types

### Blob

A blob stores file content. It does not store the file name. Create a blob from a file and print its identifier:

```text
git hash-object -w notes.txt
```

`-w` writes the object. Without it, Git only calculates the identifier.

### Tree

A tree represents one directory level. Its entries connect names and modes to blobs or other trees.

Inspect the current commit's top tree:

```text
git ls-tree HEAD
git ls-tree -r HEAD
```

### Commit

A commit object names a top-level tree, parent commit or commits, author, committer, and message. It does not contain a patch directly. Git produces a patch by comparing snapshots.

```text
git cat-file -p HEAD
```

### Annotated tag

An annotated tag object names another object and stores tagger information and a message. A lightweight tag is only a reference and does not create this tag object.

## Inspect object type and size

```text
git cat-file -t OBJECT
git cat-file -s OBJECT
git cat-file -p OBJECT
```

The pretty form understands the object's structure. Do not manually edit object files.

## References give objects useful names

A local branch such as `refs/heads/main` stores the identifier of its current commit. A tag is under `refs/tags/`. A remote-tracking name is under `refs/remotes/`.

Resolve names:

```text
git rev-parse HEAD
git rev-parse main
git show-ref
```

References may be stored in individual files or combined in packed reference storage. Use Git commands instead of assuming a particular internal file exists.

## HEAD connects the working state

During normal branch work, `HEAD` is a symbolic reference to a branch such as `refs/heads/main`. During detached work, it contains an object identifier directly.

```text
git symbolic-ref -q HEAD
```

An unsuccessful result while detached is expected.

## Why a commit changes when metadata changes

The commit identifier depends on the complete commit object, including tree, parents, author, committer, and message. This explains why amend, rebase, and cherry-pick create new identities even when much of the file content is unchanged.

## Common mistakes

### Saying a commit stores only changed lines

A commit names a full tree snapshot. Diffs are comparisons between snapshots.

### Saying a blob knows its file name

Trees associate names with blob identifiers.

### Editing `.git` to learn faster

Use read-only plumbing commands in disposable repositories. Manual edits can corrupt repository state.

## Check your understanding

You are ready when you can trace a branch to a commit, its tree, and a named file's blob.
