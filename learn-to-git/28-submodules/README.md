# Module 28: Manage Nested Repositories with Submodules

## What you will learn

You will understand what a submodule records, clone it correctly, update its checked-out commit, and record that update in the parent repository.

## Why submodules exist

A project may need another independently versioned Git repository at a path inside its working tree. A submodule lets the parent repository record one exact commit from that other repository.

The parent does not copy the child repository's full history into its own commits. It records:

- A special tree entry called a gitlink that names the chosen child commit
- Configuration in `.gitmodules`, including the submodule path and URL

This exact pointer makes builds repeatable, but updating the child and updating the parent are separate actions.

## Add a submodule

From the parent repository:

```text
git submodule add URL_OR_PATH vendor/library
git status
git diff --staged --submodule
git commit -m "Add library submodule"
```

The commit records `.gitmodules` and the selected child commit at `vendor/library`.

Local file paths may be blocked by Git's transport security defaults. For a disposable local lab only, allow that protocol for one command rather than changing a global setting:

```text
git -c protocol.file.allow=always submodule add ../library.git vendor/library
```

Do not weaken global protocol rules to make an unknown repository work.

## Clone a project with submodules

The easiest complete clone is:

```text
git clone --recurse-submodules PARENT_URL parent-copy
```

If the parent was already cloned:

```text
git submodule update --init --recursive
```

This initializes known submodules and checks out the exact commits recorded by the parent. A submodule is commonly in detached `HEAD` at that recorded commit. This is normal for reproducing the parent snapshot.

## Update the recorded child commit

First decide which child branch or commit the project should use. Inside the submodule, fetch and check out that intended child commit according to its workflow. Then return to the parent:

```text
git status
git diff --submodule
git add vendor/library
git commit -m "Update library submodule"
```

The parent commit stores the new gitlink. Teammates can run submodule update to check out that exact child commit.

## Make changes to the child deliberately

If you intend to develop the child repository:

1. Enter the submodule.
2. Switch to or create a real child branch.
3. Commit and publish through the child repository's remote.
4. Return to the parent.
5. Stage and commit the updated child pointer.

Publishing only the parent pointer is not enough if other people cannot fetch the child commit.

## Inspect status recursively

```text
git submodule status --recursive
git status
git diff --submodule
```

A leading `-` in submodule status means not initialized, `+` means the checked-out child commit differs from the parent record, and `U` means merge conflicts.

## Common mistakes

### Committing inside the child but not the parent pointer

The parent still records the old child commit until you stage the submodule path there.

### Committing a parent pointer to an unavailable child commit

Publish the child commit to an accessible remote first.

### Treating a submodule like an ordinary folder

It is a separate repository with its own branches, remotes, status, and history.

## Check your understanding

You are ready when you can explain the gitlink, initialize a cloned submodule, and perform both child and parent steps of an update.
