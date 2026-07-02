# Option 07: Pure TypeScript Version Control Engine (Mini-Git)

**Difficulty:** Expert
**Primary Concepts:** Data modeling, tree/graph traversal, immutability, classes, file I/O or in-memory simulation

---

## Why This Matters

Git is the backbone of modern software engineering. Underneath the CLI commands (`add`, `commit`, `branch`, `checkout`), Git is a **content-addressable Directed Acyclic Graph (DAG)**. Building a mini version of Git in TypeScript forces you to master immutable data structures, pointer manipulation, and deep object cloning without relying on third-party libraries.

---

## Domain Architecture

You must model Git's core internal objects
```typescript
// A Blob stores raw file content
interface BlobObject {
  type: "blob";
  hash: string;         // SHA-256 or simple simulated hash of content
  content: string;
}

// A Tree maps filenames to Blobs or sub-Trees
interface TreeEntry {
  mode: "file" | "dir";
  name: string;
  hash: string;
}

interface TreeObject {
  type: "tree";
  hash: string;
  entries: TreeEntry[];
}

// A Commit points to a root Tree and parent Commits
interface CommitObject {
  type: "commit";
  hash: string;
  treeHash: string;     // Root tree representing the repository state
  parentHashes: string[]; // 0 parents for root commit, 1 for normal, 2+ for merge
  author: string;
  message: string;
  timestamp: number;
}

type GitObject = BlobObject | TreeObject | CommitObject;
```

---

## Core Requirements

Build a `MiniGit` class supporting
```typescript
init(): void
// Initializes repository with a 'master' branch pointing to null, and HEAD pointing to 'master'.

add(filename: string, content: string): BlobObject
// Stages a file in the staging area (index).

commit(message: string, author: string): CommitObject
// Creates Tree objects from staged files, creates a Commit pointing to current parent,
// advances current branch pointer, and clears staging area.

log(): CommitObject[]
// Traverses parent pointers starting from current HEAD and returns chronological commit history.

branch(branchName: string): void
// Creates a new branch pointer at current HEAD commit.

checkout(target: string): { branch: string; commit: CommitObject; files: Record<string, string> }
// Switches HEAD to a branch or specific commit hash.
// Reconstructs full file working directory map from the root Tree.

diff(commitHashA: string, commitHashB: string): string[]
// Returns list of filenames added, modified, or deleted between two commits.
```

---

## Error Handling Rules

Create custom errors for all illegal operations
- `DetachedHeadError` (trying to commit while checked out directly to a commit hash instead of a branch).
- `BranchExistsError` / `BranchNotFoundError`.
- `NothingToCommitError` (running commit when staging area is empty).

---

## What Your Final index.ts Should Demonstrate

1. Initialize repository and create two files (`README.md` and `app.ts`).
2. Stage and commit both files.
3. Create a branch called `feature-login` and switch to it.
4. Modify `app.ts`, add `login.ts`, stage, and commit.
5. Check out `master` branch and verify `login.ts` disappears from reconstructed working files.
6. Print the `diff` between `master` and `feature-login`.
