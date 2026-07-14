# Exercises: Investigate with Log, Blame, and Bisect

## Exercise 1: Search content history

1. In a course repository with several edits, search for the commit where a known exact line appeared using `-S`.
2. Show the patch for that result.
3. Search the same file using a simple `-G` expression that matches two variants.
4. Explain why the result sets may differ.

## Exercise 2: Follow one current line

1. Run blame on a tracked text file.
2. Limit it to one or two lines with `-L`.
3. Inspect the named commit with show.
4. Read its parent version and explain the full change in context.

## Exercise 3: Bisect controlled history

1. Create `bisect-practice` with five commits. In commits one through three, `state.txt` says `good`. In commits four and five, it says `bad`.
2. Start bisect with commit five as bad and commit one as good.
3. At each checked-out commit, read the file and mark good or bad.
4. Record the first bad commit reported by Git.
5. Reset bisect and confirm you returned to `main`.
