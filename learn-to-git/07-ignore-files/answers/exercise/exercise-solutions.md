# Exercise Solutions: Ignore Generated and Private Files

## Exercise 1

After creating the files and folder:

```text
git status --short
git status --ignored --short
git check-ignore -v debug.log
git check-ignore -v .env
git check-ignore -v build/result.txt
```

Normal status should omit ignored paths. The ignored view marks them with `!!`.

## Exercise 2

Add these lines in this order:

```text
*.cache
!important.cache
```

Then run `git status --short`. `important.cache` should appear and `temporary.cache` should not.

## Exercise 3

```text
git add .gitignore important.cache
git diff --staged
git commit -m "Add shared ignore rules"
git status --short
```

Ignored practice files remain on disk but stay out of normal status.
