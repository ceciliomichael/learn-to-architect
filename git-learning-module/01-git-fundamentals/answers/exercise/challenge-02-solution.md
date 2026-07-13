# Challenge 02: Framing the Shot (Solution)

## Explanation
In this scenario, we must explicitly control which files are moved from the Working Directory into the Staging Area.

### Step-by-Step Breakdown

1. **Creating the Files**
On macOS, Linux, or Git Bash:

```bash
touch index.html app.js notes.txt
```

In PowerShell:

```powershell
New-Item index.html, app.js, notes.txt -ItemType File
```
These files are now present in the Working Directory (the "Workshop").

2. **Staging Specific Files**
```bash
git add index.html
git add app.js
```
Alternatively, you can chain them in a single command:
```bash
git add index.html app.js
```
* `git`: The core program command.
* `add`: The sub-command instructing Git to move the specified file from the Working Directory to the Staging Area (the "Viewfinder").
* `index.html` and `app.js`: The precise targets we want to stage. We deliberately omit `notes.txt`.

3. **Verifying the Status**
```bash
git status
```
When running this command, Git will output two distinct lists:
* "Changes to be committed": This will list `index.html` and `app.js` (often in green), indicating they are successfully placed in the Staging Area and ready to be photographed.
* "Untracked files": This will list `notes.txt` (often in red), indicating it is still sitting in the Working Directory and will be ignored during the next commit.
