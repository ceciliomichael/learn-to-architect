# Challenge 01: Initializing and Checking Status (Solution)

## Explanation
To begin version control on a project, we must first tell Git to start monitoring the directory.

### Step-by-Step Breakdown

1. **Creating and Navigating into the Directory**
```bash
mkdir my-new-project
cd my-new-project
```
This creates a standard, untracked folder on your file system and moves your terminal session inside it.

2. **Initializing the Repository**
```bash
git init -b main
```
* `git`: The core version control program command.
* `init`: The specific sub-command instructing Git to initialize a new repository. This creates a hidden `.git` folder within your current directory, which serves as the "Photo Album" for your snapshots.
* `-b main`: Gives the initial branch the consistent name `main`, which the later course modules use.

For older Git versions that do not support `-b`, use `git init` followed by `git branch -M main`.

3. **Creating the File**
On macOS, Linux, or Git Bash:

```bash
touch readme.txt
```

In PowerShell:

```powershell
New-Item readme.txt -ItemType File
```
This creates a new, empty file in your Working Directory (the "Workshop").

4. **Checking the Status**
```bash
git status
```
* `git`: The core program command.
* `status`: The sub-command that provides a diagnostic report of the repository state. Git will report that `readme.txt` is an "untracked file", meaning it exists in the Workshop but Git has not yet been instructed to track its history or frame it in the Staging Area.
