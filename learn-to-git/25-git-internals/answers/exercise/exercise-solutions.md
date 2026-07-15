# Exercise Solutions: Objects, Trees, Commits, and References

## Exercise 1

```text
git rev-parse HEAD
git cat-file -t HEAD
git cat-file -p HEAD
git cat-file -t TREE_HASH
git cat-file -p TREE_HASH
git cat-file -t BLOB_HASH
git cat-file -p BLOB_HASH
```

The path is branch reference to commit, commit to tree, and tree entry to blob.

## Exercise 2

```text
git rev-parse main
git rev-parse HEAD
git symbolic-ref -q HEAD
git show-ref
git tag light-practice
git cat-file -t light-practice
git tag -a annotated-practice -m "Practice annotated tag"
git cat-file -t refs/tags/annotated-practice
```

On main, the first two identifiers match. The lightweight name resolves to a commit. The annotated tag reference directly identifies a tag object.

## Exercise 3

After creating identical files:

```text
git hash-object first-copy.txt
git hash-object second-copy.txt
```

The identifiers match because object identity depends on type and content, not path. After changing one byte, its calculated identifier differs.
