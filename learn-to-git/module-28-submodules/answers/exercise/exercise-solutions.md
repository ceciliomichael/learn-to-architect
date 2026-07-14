# Exercise Solutions: Manage Nested Repositories with Submodules

## Exercise 1

Create files with an editor at the stated steps:

```text
mkdir library-source
cd library-source
git init
git add library.txt
git commit -m "Add library content"
cd ..
git clone --bare library-source library.git
mkdir parent-project
cd parent-project
git init
git add README.md
git commit -m "Start parent project"
```

## Exercise 2

```text
git -c protocol.file.allow=always submodule add ../library.git vendor/library
git status
git diff --staged --submodule
git commit -m "Add local library submodule"
git ls-tree HEAD vendor/library
```

The tree entry mode should be `160000`, which represents a gitlink.

## Exercise 3

From the folder containing `parent-project`:

```text
git -c protocol.file.allow=always clone --recurse-submodules parent-project parent-copy
cd parent-copy
git submodule status --recursive
```

After creating and committing the second version in `library-source`:

```text
git push ../library.git main
cd ../parent-project/vendor/library
git fetch origin
git switch --detach origin/main
cd ../..
git status
git diff --submodule
git add vendor/library
git commit -m "Update library submodule"
```

The parent commit now records the second child commit.
