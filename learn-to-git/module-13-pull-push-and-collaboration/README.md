# Module 13: Pull, Push, and Collaborate Safely

## What you will learn

You will integrate fetched work, push a branch, handle a rejected push, and follow a calm collaboration routine.

## Integrate after inspection

After fetch shows that `origin/main` is ahead, bring it into local `main` with the merge skills you already learned:

```text
git switch main
git merge origin/main
```

If local `main` has no unique commits, this is normally a fast-forward.

## What pull does

`git pull` first fetches and then integrates the fetched branch into the current branch. The integration method depends on options and configuration.

Choose it explicitly when learning:

```text
git pull --ff-only
git pull --no-rebase
git pull --rebase
```

- `--ff-only` succeeds only when the local branch can move straight forward.
- `--no-rebase` uses merge when histories diverge.
- `--rebase` replays local commits after the fetched commits. Rebase is taught in Module 19.

For a beginner, `fetch`, inspect, then `merge` makes each stage visible. Pull becomes convenient once you can predict the result.

## Push local commits

```text
git push origin main
```

This asks Git to update `main` in `origin` using local `main` and sends required objects. The remote may reject the update because of permissions, policy, or history that you do not have.

For a new local branch, publish it and set its upstream:

```text
git push -u origin topic
```

Afterward, plain `git push` and `git pull` can use the configured upstream, subject to Git configuration.

## Respond to a non-fast-forward rejection

A common rejection means the remote branch contains work not reachable from your local branch. Do not force immediately.

Use this routine:

```text
git fetch origin
git log --graph --oneline --decorate --all
git log --oneline main..origin/main
git log --oneline origin/main..main
git merge origin/main
```

Resolve and test if necessary, then push again. A protected main branch may require a review request instead of direct push.

## A safe collaboration loop

1. Start with a clean working tree.
2. Fetch and inspect shared changes.
3. Integrate according to team policy.
4. Create a focused branch and commits.
5. Test the result.
6. Fetch again before publishing if others may have changed the target.
7. Push the branch.
8. Use the team's review and merge process.

## About force push

A force push can replace a remote branch's reachable history and disrupt other contributors. This course does not use it on shared branches. Later private-history modules explain when rewritten personal branches may need `--force-with-lease`, which checks expected remote state before updating.

## Common mistakes

### Pulling without knowing the current branch

Pull integrates into the current branch. Check it first.

### Force pushing after a rejection

A rejection protects remote work. Fetch and inspect the difference.

### Assuming a successful push updated every branch

Push updates only the references described by its refspec or defaults.

## Check your understanding

You are ready when you can explain pull as two stages, publish a branch, and recover calmly from a normal rejected push.
