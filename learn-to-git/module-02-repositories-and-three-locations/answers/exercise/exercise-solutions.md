# Exercise Solutions: Repositories and Git's Three Locations

## Exercise 1

```text
mkdir three-locations
cd three-locations
pwd
git init
git rev-parse --show-toplevel
git status
```

The repository root should be the `three-locations` folder. Status should name `main` and report that there are no commits yet.

## Exercise 2

Create `notes.txt` with an editor, then run:

```text
git status
```

Git lists it as an untracked file.

## Exercise 3

```text
git add notes.txt
git status
```

After editing the file again:

```text
git status
```

The file appears once under changes to be committed and again under changes not staged for commit. Stage the latest content:

```text
git add notes.txt
git status
```

Only the staged entry remains because the index and working tree now contain the same file content.
