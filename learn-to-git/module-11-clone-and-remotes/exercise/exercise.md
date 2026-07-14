# Exercises: Clone Repositories and Understand Remotes

## Exercise 1: Build a local collaboration lab

1. Go to `git-course-practice`.
2. Use your clean `branch-practice` repository as the source.
3. Create a bare clone named `shared-project.git`.
4. Clone that bare repository into `alice` and `bob`.

If those names already exist, remove only disposable lab folders after verifying their full paths, or choose fresh names and use them consistently.

## Exercise 2: Inspect Alice

1. Enter `alice`.
2. Confirm its repository root and current branch.
3. List remotes and their locations.
4. Ask for detailed information about `origin`.
5. Confirm Alice has the expected project files and history.

## Exercise 3: Prove clones are independent

1. In Alice, create an untracked `alice-only.txt`.
2. Inspect Alice's status.
3. Enter Bob and inspect Bob's files and status.
4. Confirm the untracked Alice file did not appear in Bob.
5. Delete the untracked practice file in Alice using normal file tools.
