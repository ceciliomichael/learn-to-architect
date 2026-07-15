# Module 29: Maintain Large and Long-Lived Repositories

## What you will learn

You will inspect repository storage, verify object connectivity, understand safe maintenance, and prevent avoidable repository growth.

## Git already performs routine maintenance

Git often runs lightweight automatic maintenance after ordinary commands. It can pack loose objects, update supporting indexes, and remove eligible unreachable data after grace periods.

Do not run aggressive cleanup merely because a repository has many files. Measure a real problem and keep backups before manual maintenance.

## Inspect object storage

```text
git count-objects -vH
```

This reports loose object counts and sizes, packed object information, and other storage values in readable units. A loose object is stored individually. Packfiles compress many objects together and store related content efficiently.

List packfiles through Git's resolved path rather than assuming folder layout:

```text
git rev-parse --git-path objects/pack
```

## Verify connectivity and validity

```text
git fsck
```

`fsck` checks object connectivity and validity. Messages about dangling objects can be normal after resets, rebases, or amended commits. Missing or corrupt objects need careful investigation and restoration from a healthy clone or backup.

Do not delete reported objects manually.

## Run standard garbage collection

```text
git gc
```

Standard garbage collection consolidates objects and performs normal cleanup according to configured safety periods. Avoid `--prune=now` in an active repository. Immediate pruning removes recovery opportunities and can be unsafe alongside concurrent Git processes.

## Scheduled maintenance

Modern Git provides maintenance tasks suited to frequently used and large repositories:

```text
git maintenance run
git maintenance start
```

`run` performs configured maintenance for the current repository. `start` registers scheduled maintenance using the platform's scheduler. Whether background registration is appropriate depends on the machine, repository policy, and installed Git version.

Inspect configuration before changing it:

```text
git config --show-origin --get-regexp "^maintenance\."
```

## Prevent large history instead of repairing it later

Git keeps committed file versions. Deleting a large file in a later commit does not remove its old blobs from history.

Good prevention includes:

- Ignore reproducible build and dependency output.
- Review staged file sizes before committing.
- Store generated archives and releases in artifact storage.
- Use a team-approved large-file system such as Git LFS when appropriate.
- Never commit secrets. Rotate an exposed secret even if history will be rewritten.

Rewriting old history to remove large or secret files changes many commit hashes. It requires backups, a suitable history-filtering tool, a coordinated force update, and instructions for every clone. Treat it as a separate migration, not routine cleanup.

## Shallow and partial clones

For very large remote repositories, a team may use shallow clones or partial clones:

```text
git clone --depth=1 URL
git clone --filter=blob:none URL
```

A shallow clone has limited history and some operations behave differently until more history is fetched. A partial clone asks a capable server to delay some object downloads until needed. Use these only when the project supports the workflow.

## A healthy repository routine

1. Keep important work on named branches and trusted remotes.
2. Maintain tested backups of critical repositories.
3. Use protected shared branches and continuous integration.
4. Delete merged branch names according to team policy, while remembering that branch names are tiny and are not the main source of object growth.
5. Investigate unusual size with `count-objects`, object listing tools, and server reports before rewriting anything.
6. Upgrade Git through approved system processes so fixes and performance improvements remain current.

## Common mistakes

### Expecting branch deletion to shrink history immediately

Objects reachable from other references remain needed, and unreachable objects are kept for recovery periods.

### Running immediate prune to save a small amount of space

The lost recovery window is usually more costly. Use default safe expiration and measured maintenance.

### Treating a later secret deletion as enough

The old commit still contains it. Rotate the credential first, then coordinate any required history cleanup.

## Check your understanding

You are ready when you can inspect storage and integrity, explain what normal maintenance does, and identify when repository cleanup becomes a coordinated migration.
