# Exercises: Pull, Push, and Collaborate Safely

Continue with Bob one commit behind `origin/main`.

## Exercise 1: Integrate the fetched commit

1. In Bob, confirm `main` is current and the working tree is clean.
2. Inspect the graph.
3. Merge `origin/main` into `main`.
4. Confirm `team.txt` now exists and the graph is fast-forwarded.

## Exercise 2: Publish Bob's work

1. In Bob, create and switch to `bob-note`.
2. Create `bob.txt`, commit it, and push with upstream setup.
3. Inspect verbose branches and remote-tracking branches.
4. Switch back to `main`.

## Exercise 3: Observe and solve a rejected push

1. In Alice on `main`, append `Alice update.` to `team.txt`, commit, and push.
2. In Bob on `main`, without fetching first, append `Bob update.` on a different line, commit, and try to push.
3. Read the rejection. Fetch and inspect both unique commit sets.
4. Merge `origin/main`, resolve if your edits conflict, and inspect the result.
5. Push again and verify that local `main` and `origin/main` match.
