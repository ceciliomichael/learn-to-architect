# Question 02 (Answer)

We use `git add` before `git commit` to achieve explicit, granular control over our version history.

If Git only had a single "save everything" command, every commit would be a chaotic mixture of finished features, half-written functions, and temporary debug files. By decoupling the act of selecting changes (`git add`) from the act of recording changes (`git commit`), Git provides immense **architectural control**.

This two-step process allows developers to logically group related modifications. For example, if you spend two hours working and modify ten files (some for a database fix, some for a UI enhancement), you do not want to bundle them all into one massive commit. You can use `git add` to stage only the database files, run `git commit -m "Fix database connection"`, and then use `git add` for the UI files, followed by `git commit -m "Enhance navigation bar"`. This creates a clean, semantic history that is easy for other engineers to review or revert if necessary.
