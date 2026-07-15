# Exercises: Manage Nested Repositories with Submodules

Use only disposable local repositories.

## Exercise 1: Prepare a local library

1. Create `library-source`, initialize it, add `library.txt`, and commit.
2. From the parent folder, create a bare clone named `library.git`.
3. Create `parent-project`, initialize it, add `README.md`, and commit.

## Exercise 2: Add and inspect the submodule

1. In `parent-project`, add `../library.git` at `vendor/library` using the one-command local protocol allowance shown in the lesson.
2. Inspect status and the staged submodule diff.
3. Commit `.gitmodules` and the gitlink.
4. Show the parent tree entry for `vendor/library` and notice its special mode.

## Exercise 3: Clone and update

1. Clone the parent to `parent-copy` with recursive submodules and a one-command local protocol allowance: `git -c protocol.file.allow=always clone --recurse-submodules parent-project parent-copy`.
2. Inspect recursive submodule status.
3. In `library-source`, make a second commit and push it to `library.git`.
4. In `parent-project/vendor/library`, fetch and move to the new library commit.
5. In `parent-project`, stage and commit the new submodule pointer.
