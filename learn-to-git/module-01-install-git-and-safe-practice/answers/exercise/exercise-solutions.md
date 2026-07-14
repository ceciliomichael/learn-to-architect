# Exercise Solutions: Install Git and Create a Safe Practice Area

## Exercise 1

```text
pwd
git --version
git config --global --get user.name
git config --global --get user.email
```

If values are missing:

```text
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Use your own values. A missing `--get` result usually prints nothing.

## Exercise 2

From the parent folder where you want to keep the course:

```text
mkdir git-course-practice
cd git-course-practice
pwd
```

The displayed path should end in `git-course-practice`.

## Exercise 3

```text
git config --global init.defaultBranch main
git config --global --get init.defaultBranch
```

The final command should print `main`.
