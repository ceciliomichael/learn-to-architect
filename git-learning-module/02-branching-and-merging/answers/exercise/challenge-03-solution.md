# Solution for Challenge 03: The Merge Conflict

Merge conflicts are standard occurrences in collaborative enterprise environments. Here is the rigorous, step-by-step technical approach to handling them.

### 1. Initial State Setup
```bash
echo "ServerPort = 8080" > config.txt
git add config.txt
git commit -m "Add initial server config"
```

### 2 & 3. Branching and Editing Timeline A
Create the parallel universe and alter the specific configuration line.
```bash
git switch -c feature-config
echo "ServerPort = 9000" > config.txt
git add config.txt
git commit -m "Change port to 9000 for local testing"
```

### 4. Branching and Editing Timeline B (Divergence)
Return to the primary timeline and intentionally alter the exact same line in a conflicting manner.
```bash
git switch main
echo "ServerPort = 80" > config.txt
git add config.txt
git commit -m "Update port to standard HTTP 80"
```

### 5. Attempting the Merge
Trigger the conflict by attempting to absorb `feature-config` into `main`.
```bash
git merge feature-config
```
Git halts. The terminal outputs an error explicitly stating a merge conflict exists in `config.txt` and automatic merging has failed.

### 6. Resolving the Conflict
Open `config.txt` in your code editor. You will see Git's conflict markers injected directly into the file syntax.

```text
<<<<<<< HEAD
ServerPort = 80
=======
ServerPort = 9000
>>>>>>> feature-config
```

**Understanding the Markers:**
* `<<<<<<< HEAD`: This line indicates the beginning of the block of code from your *current* timeline (`main`).
* `=======`: The dividing line. Everything above this comes from your current branch, and everything below comes from the branch you are attempting to merge.
* `>>>>>>> feature-config`: This indicates the end of the block from the incoming timeline.

**The Resolution Action:**
You must manually delete these syntax markers and leave only the code you wish to persist. Suppose you decide the production standard (port 80) is correct. You edit the file to look exactly like this:
```text
ServerPort = 80
```

Finally, you must explicitly tell Git that the human intervention is complete. You do this by staging the resolved file and finalizing the merge with a commit.
```bash
git add config.txt
git commit -m "Merge feature-config, resolving port conflict in favor of standard HTTP"
```

**Real-World Analogy:**
Imagine two separate architects holding identical blueprints of a house. Architect A erases the kitchen door and draws a window. Architect B erases the exact same kitchen door and draws a sliding glass wall. When they attempt to lay the blueprints on top of each other (merging), they cannot logically combine a window and a glass wall in the exact same physical space. Git behaves like a project manager; it circles the contradictory area in red marker, hands it back to the architects, and says, "I am just a machine. You two humans figure out what goes here, erase my red circles, and give me the final, decided blueprint."
