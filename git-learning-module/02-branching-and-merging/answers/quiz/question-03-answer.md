# Answer to Question 03

**What is the Golden Rule of Merging?**

The Golden Rule of Merging dictates that you must ALWAYS travel to the specific timeline you want to pull the incoming code *into* before you execute the merge operation.

Git merges are inherently directional; they pull commits from an external branch into the currently checked-out branch.

If you intend to bring new features from a branch named `feature-ui` into your stable `main` branch, you must guarantee that your active working directory is `main`. You execute `git switch main` first, securely positioning yourself in the destination universe, and only then do you execute `git merge feature-ui`.
