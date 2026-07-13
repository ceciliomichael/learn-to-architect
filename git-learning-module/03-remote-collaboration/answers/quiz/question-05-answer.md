# Question 05 Answer

**Correct Answer:** C) `git fetch origin`

## Exhaustive Explanation

In this scenario, the primary constraint is that you possess "highly experimental, uncommitted code". Your Working Directory is dirty and vulnerable.

If you execute `git pull origin main`, Git will download the senior engineer's new commits and immediately attempt to integrate them into your current branch. If that would overwrite local uncommitted changes, Git normally aborts and asks you to commit or stash them. Either way, `pull` is the wrong command when your goal is to inspect without integrating.

By executing `git fetch origin`, you exercise strict architectural control.

Git will download the senior engineer's commits, but it will quarantine them in the `origin/main` tracking branch. Your Working Directory remains completely untouched. Your experimental code is safe.

Once the `fetch` is complete, you can safely run commands like `git log origin/main` or `git diff main origin/main` to meticulously review the senior engineer's work. You can then choose to finish your experimental work, commit it, and *then* manually merge the remote changes on your own terms.
