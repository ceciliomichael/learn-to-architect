# Exercises: Maintain Large and Long-Lived Repositories

Use a disposable repository with several commits.

## Exercise 1: Measure before maintenance

1. Run the object count with human-readable sizes.
2. Record loose and packed object counts.
3. Ask Git for the pack directory path.
4. Run the standard integrity check and read every message.

## Exercise 2: Run safe standard maintenance

1. Make a normal copy or bare clone of the disposable repository as a backup.
2. Run standard `git gc` without aggressive or immediate-prune options.
3. Run the object count again.
4. Run `git fsck` again.
5. Compare results without assuming the small practice repository must shrink.

## Exercise 3: Find growth risks

1. Review `.gitignore` and identify generated paths the project should exclude.
2. List tracked files and identify any unexpected archive, media, database, or build output.
3. Inspect recent staged and committed statistics.
4. Write a short maintenance note describing what belongs in Git, what belongs in artifact storage, and what would require Git LFS or another approved system.
