# Module 01: Git Fundamentals

Welcome to the foundation of version control. In this module, we will explore the core mechanics of Git. We will not look at GitHub or internet servers yet; we are going to focus purely on how Git operates locally on your own computer.

---

## 1. The Core Concept: The Photography Studio Analogy

When learning Git, beginners often confuse it with a cloud backup system like Google Drive. **This is a dangerous misconception.** Git does not constantly sync your files in the background. You must manually tell Git exactly what to save and when to save it.

To understand Git, imagine you are a photographer running a professional **Photography Studio**.

Your studio has three distinct rooms:
1. **The Workshop (Working Directory):** This is where you physically build your sets, move props around, and adjust the lighting. It is messy, chaotic, and constantly changing.
2. **The Viewfinder (Staging Area / Index):** This is where you frame your exact shot. You might have ten props in the workshop, but you only want three of them in the final photograph. You move those three props into the camera's viewfinder.
3. **The Photo Album (The Repository / HEAD):** This is the permanent, indestructible photo album. Once you press the shutter button, the exact image in the viewfinder is printed and locked into the album forever with a timestamp.

In Git terminology, moving code from the Workshop to the Viewfinder is called **Staging** (`git add`). Pressing the shutter button to save the picture into the Photo Album is called **Committing** (`git commit`).

---

## 2. Setting Up the Studio (`git init -b main`)

Before you can take any photographs, you need to buy a camera and set up the studio.

When you create a new folder for a coding project, it is just a normal folder. To tell Git to start tracking this folder and give its first branch the course-standard name `main`, run:

```bash
git init -b main
```

### Syntax Breakdown: `git init -b main`
* `git`: The built-in software program we are running. Every Git command starts with this keyword.
* `init`: Short for "initialize." This built-in command tells Git to create a hidden `.git` folder inside your project. This hidden folder is your actual "Photo Album."
* `-b main`: Names the initial branch `main`, so every later module can use the same branch name on every machine.

If your Git version does not support `-b`, run `git init` followed by `git branch -M main`.

**Pre-emptive Pitfall Warning:** You only ever initialize a repository **once** per project! If you initialize repositories inside nested folders, you will create confusing inception-like histories.

---

## 3. Looking Around the Studio (`git status`)

As you work, you will frequently want to know the current state of your workshop. Are there new props? Have you framed anything in the viewfinder yet?

You check this using the status command.

### Syntax Breakdown: `git status`
* `git`: The core program.
* `status`: The built-in command that prints out a diagnostic report of your three rooms (Working Directory, Staging Area, and Repository).

Running `git status` is perfectly safe. It does not change any files. You should run this command constantly as a beginner to understand what Git sees.

---

## 4. Framing the Shot (`git add`)

Imagine you just created three new files: `index.html`, `styles.css`, and a scratchpad file called `secret-notes.txt`.

You only want `index.html` and `styles.css` to be part of your official project snapshot. You do not want `secret-notes.txt` included.

You must manually move the files you want into the Staging Area.

### Syntax Breakdown: `git add <filename>`
* `git add`: The built-in command to move a file from the Working Directory into the Staging Area.
* `<filename>`: The made-up name of your specific file.

```bash
# Example: Staging two specific files
git add index.html
git add styles.css
```

### The "Add Everything" Shortcut
If you want to move every single changed file in your entire workshop into the viewfinder at once, you can use the period (`.`) wildcard.

```bash
git add .
```
**Engineering Motivation:** Why does the Staging Area even exist? Why not just save everything at once? The staging area gives you architectural control. It allows you to logically group related changes together. If you fixed a bug in `login.ts` and wrote a new feature in `cart.ts`, you can stage and save them as two separate, logically distinct snapshots rather than one giant, confusing mess.

---

## 5. Pressing the Shutter Button (`git commit`)

Once your files are framed perfectly in the Staging Area, it is time to press the shutter button and save them permanently into the repository.

### Syntax Breakdown: `git commit -m "Your Message"`
* `git commit`: The built-in command that takes everything currently in the Staging Area and permanently saves it into the `.git` photo album.
* `-m`: A built-in "flag" (short for message) that allows you to attach a descriptive label directly in the command line.
* `"Your Message"`: Your custom, human-readable description of what this snapshot contains.

```bash
# Example: Creating a permanent snapshot
git commit -m "Add the homepage HTML structure and CSS styling"
```

### The Anatomy of a Commit
When you press the shutter button, Git generates a completely unique receipt number for that snapshot, called a **SHA-1 Hash** (e.g., `a1b2c3d4e5f6...`). This hash mathematically guarantees that nobody can ever silently alter the code in that snapshot without the receipt number changing.

---

## 6. Reviewing the Photo Album (`git log`)

After making several commits, you will want to look back at your project's timeline to see all the snapshots you have taken.

### Syntax Breakdown: `git log`
* `git log`: The built-in command that prints the chronological history of your repository.

When you run this command, Git will list every commit, showing you:
1. The unique SHA-1 Hash receipt.
2. The author who wrote the code.
3. The exact timestamp.
4. The custom message you wrote.

*(Note: If the log history is very long, it will open in a reader mode. You can press the `q` key on your keyboard to quit the reader and return to your normal terminal).*

---

## 7. The Golden Rule and Common Pitfalls

### The "Forgot to Stage" Pitfall
The most common mistake beginners make is editing a file, forgetting to run `git add`, and immediately running `git commit -m "Update file"`.

If you do this, Git will tell you `no changes added to commit`.
Why? Because your edited file is still sitting in the Workshop. It was never moved into the Viewfinder. You cannot take a picture of a prop that isn't in front of the camera!

**The Golden Workflow:**
1. Work on your files.
2. Run `git status` to see what changed.
3. Run `git add .` (or specific filenames) to stage the files.
4. Run `git status` again to verify they are staged (they will usually appear in green text).
5. Run `git commit -m "Descriptive message"` to save the snapshot.
