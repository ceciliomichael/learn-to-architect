# Module 02: Branching and Merging

Welcome to Module 02. In the first module, we learned how to save linear snapshots of our code. But what if you want to experiment with a risky new feature without breaking the stable code that currently works?

This is where **Branching** comes in.

---

## 1. The Core Concept: Parallel Universes

Imagine you are writing a famous novel. You reach Chapter 5, and you have two different ideas for how the story should end. You don't want to delete your current work, but you want to try writing both endings to see which is better.

In Git, you can create a **Branch**. A branch is a parallel universe. It is an exact clone of your project at a specific point in time. You can switch to this new universe, make changes, and save commits. Meanwhile, your original, stable universe remains completely untouched.

If you like the new ending, you can **Merge** the parallel universe back into the main one. If you hate it, you can delete the parallel universe, and it is like it never happened.

---

## 2. Viewing and Creating Branches (`git branch`)

By default, every Git repository starts with one primary branch. This is your main timeline. Historically, this was called `master`, but modern systems typically call it `main`.

### Syntax Breakdown: `git branch`
* `git branch`: Running this command with no other words will list all the parallel universes that currently exist in your project. The one you are currently standing in will have an asterisk (`*`) next to it.

### Creating a New Universe
To create a new branch, you provide a name.

```bash
# Example: Creating a new branch for a dark-mode feature
git branch feature-dark-mode
```

**Pre-emptive Pitfall Warning:** Running `git branch feature-dark-mode` *creates* the parallel universe, but it **does not** teleport you into it! You are still standing in `main`.

---

## 3. Traveling Between Universes (`git switch` and `git checkout`)

To actually move your workshop into the newly created parallel universe, you must switch branches.

### Syntax Breakdown: `git switch`
* `git switch <branch-name>`: This tells Git to update all the files in your Working Directory to match the exact state of the target branch.

```bash
git switch feature-dark-mode
```

*(Note: In older versions of Git, the command `git checkout feature-dark-mode` was used to switch branches. You will still see `checkout` heavily used in older tutorials, but `switch` is the modern, safer command).*

### The Shortcut: Create and Switch
You can create a branch and teleport into it immediately using a single command:
```bash
git switch -c feature-dark-mode
```
* `-c`: A built-in flag standing for "create."

---

## 4. Fusing Realities Together (`git merge`)

You have spent two days in the `feature-dark-mode` universe. You staged and committed your code. It works perfectly. Now, you want to bring those changes back into the stable `main` timeline.

**The Golden Rule of Merging:** You must ALWAYS travel to the universe you want to pull code *into* before merging.

If you want `main` to receive the new code, you must be standing in `main`.

### Step-by-Step Merge
1. Teleport back to the stable timeline:
   ```bash
   git switch main
   ```
2. Instruct Git to absorb the parallel timeline into the current one:
   ```bash
   git merge feature-dark-mode
   ```

### Syntax Breakdown: `git merge <branch-name>`
* `git merge`: The built-in command to fuse histories.
* `<branch-name>`: The made-up name of the universe you want to absorb.

---

## 5. When Universes Collide: Merge Conflicts

Sometimes, parallel universes contradict each other.

Imagine Alice is on the `main` branch and changes the background color on line 10 to `blue`. Bob is on the `feature-dark-mode` branch and changes the exact same line 10 to `black`.

When Bob tries to `git merge feature-dark-mode` into `main`, Git panics. Git is a machine; it does not know if the background should be blue or black. This is called a **Merge Conflict**.

### Resolving the Conflict
Git will pause the merge and mark the conflicting file in your code editor. It will inject special symbols directly into your code:

```text
<<<<<<< HEAD
background-color: blue;
=======
background-color: black;
>>>>>>> feature-dark-mode
```

**How to fix it:**
1. Open the file in your code editor.
2. Manually delete the Git markers (`<<<<<<<`, `=======`, `>>>>>>>`).
3. Keep the code you want (e.g., leave only `background-color: black;`).
4. Stage the resolved file: `git add .`
5. Finalize the merge by committing: `git commit -m "Resolve merge conflict for background color"`

Merge conflicts are perfectly normal. Do not panic. They are just Git politely asking a human to make an executive decision.
