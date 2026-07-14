# Exercises: Automate Local Checks with Hooks

Use Git Bash or another shell that can run POSIX shell scripts for this exercise.

## Exercise 1: Create a tracked hook

1. Create a new `hook-practice` repository with one initial commit.
2. Create `.githooks/commit-msg` containing the complete lesson script.
3. On macOS or Linux, mark it executable with `chmod +x .githooks/commit-msg`. Git Bash on Windows normally uses the script through its shell.
4. Set local `core.hooksPath` to `.githooks`.
5. Commit the hook file with an acceptable message.

## Exercise 2: Observe pass and fail

1. Make and stage a small file change.
2. Try to commit with `WIP temporary change` and read the rejection.
3. Confirm the change is still staged and no commit was created.
4. Commit again with `Add practice change`.
5. Confirm the commit succeeds.

## Exercise 3: Prove configuration is local

1. Clone `hook-practice` to a sibling folder.
2. In the clone, inspect `core.hooksPath`.
3. Confirm the tracked `.githooks/commit-msg` file exists but is not active until configured.
4. Configure it locally and repeat one rejected message.
