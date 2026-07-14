# Exercises: Configuration, Aliases, and Attributes

Use a clean disposable repository.

## Exercise 1: Trace configuration

1. Show all effective configuration with origins and scopes.
2. Find the source of `user.name`.
3. Set local `course.level` to `advanced`.
4. Read its value and source.
5. Remove it locally and confirm it is absent.

## Exercise 2: Create a readable alias

1. Add a local alias named `overview` for the decorated all-branch graph.
2. Run it.
3. List local aliases.
4. Remove the alias and confirm `git overview` no longer exists.

## Exercise 3: Apply and inspect attributes

1. Create `.gitattributes` with `* text=auto`, `*.sh text eol=lf`, and `*.png binary`.
2. Create `script.sh` and an empty practice `image.png`.
3. Ask Git for all attributes on each path.
4. Stage the attributes and practice files, inspect the diff, and commit.
