# Solution for Challenge 01: Creating a Parallel Universe

Below is the exhaustive, enterprise-grade breakdown for completing this challenge.

### 1. Determine your current branch
Before creating a new universe, you must know your current origin point.
```bash
git branch
```
**Breakdown:**
* `git`: The root executable program.
* `branch`: The subcommand that lists all local branches. The branch with the asterisk (`*`) is your active branch. You should see `* main`.

### 2 & 3. Create a new branch and switch to it
While you can run `git branch feature-auth` followed by `git switch feature-auth`, the most efficient, professional-grade approach is to use the compound command.

```bash
git switch -c feature-auth
```
**Breakdown:**
* `git`: The core version control executable.
* `switch`: The dedicated modern command for changing your active working directory state.
* `-c`: The built-in flag specifying "create". It instructs Git to instantiate a new branch pointer at the current commit before switching to it.
* `feature-auth`: The specific, semantic string identifier for your new branch.

### 4. Verify the switch
```bash
git branch
```
You will now see an output listing multiple branches, with the asterisk indicating you have safely arrived in the new timeline:
```text
* feature-auth
  main
```

**Real-World Analogy:**
Think of a Git repository as a grand library. Running `git switch -c feature-auth` is like taking a photocopy of the entire library exactly as it stands today, placing that photocopy into a brand new building named "feature-auth", and walking through the front doors of that new building to begin your work. The original library ("main") remains untouched by the renovations you make inside your new building.
