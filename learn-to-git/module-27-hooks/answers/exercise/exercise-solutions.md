# Exercise Solutions: Automate Local Checks with Hooks

## Exercise 1

After initializing and making an ordinary first commit, create `.githooks/commit-msg` with:

```text
#!/bin/sh
message_file="$1"
if grep -q "WIP" "$message_file"
then
  echo "Commit message must not contain WIP."
  exit 1
fi
exit 0
```

Then:

```text
chmod +x .githooks/commit-msg
git config core.hooksPath .githooks
git add .githooks/commit-msg
git commit -m "Add commit message check"
```

If `chmod` is not available outside Git Bash on Windows, run these steps in Git Bash.

## Exercise 2

After editing and staging a practice file:

```text
git commit -m "WIP temporary change"
git status
git log -1 --oneline
git commit -m "Add practice change"
git log -1 --oneline
```

The first commit should be rejected with the hook message. The second should succeed.

## Exercise 3

From the parent folder:

```text
git clone hook-practice hook-clone
cd hook-clone
git config --get core.hooksPath
git config core.hooksPath .githooks
```

Before local setup, the get command should print nothing. The tracked script is present, but each clone must configure the path and meet permission requirements.
