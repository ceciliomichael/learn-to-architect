# Exercises: Fetch and Remote-Tracking Branches

Use the `alice`, `bob`, and `shared-project.git` lab.

## Exercise 1: Create a remote change through Alice

1. In Alice, create `team.txt` with `Shared by Alice.`
2. Stage and commit it.
3. Run `git push origin main` to send the commit to the bare lab remote.
4. Do not enter Bob yet. Predict whether Bob's local `origin/main` changed.

The push command is used here to prepare the observation. Push behavior is taught fully in Module 13.

## Exercise 2: Fetch in Bob

1. Enter Bob and inspect the graph before fetching.
2. Confirm `team.txt` is absent.
3. Fetch from `origin`.
4. Inspect the graph again.
5. Confirm `team.txt` is still absent from Bob's working tree.
6. Show the commit unique to `origin/main`.

## Exercise 3: Inspect tracking

1. Show Bob's verbose branch list.
2. Count commits unique to `main` and `origin/main`.
3. Show the file from the remote-tracking snapshot with `git show origin/main:team.txt`.
4. Explain why Git can display that content without changing the working tree.
