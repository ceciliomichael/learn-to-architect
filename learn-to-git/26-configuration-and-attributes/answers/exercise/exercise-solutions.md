# Exercise Solutions: Configuration, Aliases, and Attributes

## Exercise 1

```text
git config --list --show-origin --show-scope
git config --show-origin --show-scope --get user.name
git config --local course.level advanced
git config --show-origin --show-scope --get course.level
git config --local --unset course.level
git config --get course.level
```

The final command should print nothing and return a nonzero status because the value is absent.

## Exercise 2

```text
git config --local alias.overview "log --graph --oneline --decorate --all"
git overview
git config --local --get-regexp "^alias\."
git config --local --unset alias.overview
```

## Exercise 3

After creating the stated paths:

```text
git check-attr -a -- script.sh
git check-attr -a -- image.png
git add .gitattributes script.sh image.png
git diff --staged
git commit -m "Define project file attributes"
```

The shell script should show text and LF attributes. The PNG should show attributes associated with the binary macro.
