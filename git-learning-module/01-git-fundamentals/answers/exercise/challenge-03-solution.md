# Challenge 03: The First Snapshot (Solution)

## Explanation
With files correctly positioned in the Staging Area, the next phase is to capture the snapshot and append it to the repository history.

### Step-by-Step Breakdown

1. **Committing the Files**
```bash
git commit -m "Initial commit with index and app files"
```
* `git`: The core program command.
* `commit`: The sub-command that executes the action of capturing everything currently in the Staging Area and saving it permanently to the repository database (the "Photo Album").
* `-m`: The flag parameter (short for message) that allows you to provide a string label inline rather than opening an external text editor.
* `"Initial commit with index and app files"`: The human-readable context explaining the architectural purpose of this snapshot.

2. **Reviewing the Timeline**
```bash
git log
```
* `git`: The core program command.
* `log`: The sub-command that queries the `.git` database and retrieves the chronological list of all previous commits.
The output will display:
* The unique SHA-1 Hash (the permanent mathematical receipt for the exact state of the files).
* The Author metadata.
* The exact timestamp of the commit.
* The message you provided via the `-m` flag.
