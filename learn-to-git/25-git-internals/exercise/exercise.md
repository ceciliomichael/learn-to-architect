# Exercises: Objects, Trees, Commits, and References

Use a clean disposable repository with at least two files and two commits.

## Exercise 1: Trace a commit

1. Resolve `HEAD` to its full object identifier.
2. Print its object type and pretty content.
3. Copy the tree identifier from the commit.
4. Print the tree type and entries.
5. Copy one blob identifier and print its content.

## Exercise 2: Connect names and objects

1. Resolve `main` and `HEAD` and compare them.
2. Print the symbolic reference for `HEAD`.
3. List all references.
4. Create a lightweight practice tag and identify whether its resolved target type is commit or tag.
5. Create an annotated practice tag and identify its direct object type with `git cat-file -t refs/tags/TAG_NAME`.

## Exercise 3: Prove identical content shares a blob

1. Create two files with exactly identical bytes.
2. Calculate each blob identifier without writing.
3. Confirm they match.
4. Change one byte in one file and calculate again.
5. Explain the new result.
