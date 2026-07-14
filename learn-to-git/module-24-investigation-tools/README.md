# Module 24: Investigate with Log, Blame, and Bisect

## What you will learn

You will search for when content changed, inspect line history, and locate a bug-introducing commit with binary search.

## Begin with a question

Investigation commands are most useful when the question is precise:

- When did this exact text appear or disappear?
- Which commits changed lines matching this pattern?
- Which commit last changed the current form of this line?
- Which commit first shows the failing behavior?

Start with a clean working tree so switching among historical commits does not risk unrelated work.

## Search by count change with `-S`

```text
git log -S"mode=unsafe" --oneline --all
git log -p -S"mode=unsafe" -- settings.txt
```

`-S` finds commits where the number of occurrences of the exact string changed. It is useful for finding when a name or literal was introduced or removed.

## Search changed lines with `-G`

```text
git log -G"mode=(safe|unsafe)" --oneline -- settings.txt
```

`-G` finds commits whose patch contains an added or removed line matching a regular expression. Use it when the text varies but follows a pattern.

## Inspect line history with blame

```text
git blame notes.txt
git blame -L 10,20 notes.txt
```

Blame annotates current lines with commits and author information. It is evidence about the last recorded change to each displayed line, not proof of fault or full ownership. A commit may have moved code, followed instructions, or exposed an older problem.

Copy a hash from blame and inspect its context:

```text
git show COMMIT
```

## Find the first bad commit with bisect

Bisect needs:

- A known bad commit where the problem occurs
- An older known good commit where it does not
- A repeatable way to classify each tested commit

Start:

```text
git bisect start
git bisect bad
git bisect good GOOD_COMMIT
```

Git checks out a commit near the middle of the candidate range. Run the same test and mark it:

```text
git bisect good
git bisect bad
```

Repeat until Git reports the first bad commit. Then return to the original branch:

```text
git bisect reset
```

If a commit cannot be tested for an unrelated reason, use `git bisect skip`. Too many skipped candidates can prevent a single answer.

## Automate a reliable test

If a script exits with status 0 for good and a value from 1 through 127 except 125 for bad, Git can run it:

```text
git bisect run ./test-script.sh
```

Exit 125 means skip this commit. The script must be deterministic and safe across the historical versions being tested.

## Common mistakes

### Picking a good commit by guess

Check out or otherwise test it before marking it good.

### Forgetting bisect changes the checked-out commit

Keep the tree clean and always finish with `git bisect reset`.

### Using blame to assign fault

Use it to find context, then read the patch, surrounding history, and discussion.

## Check your understanding

You are ready when you can choose between `-S` and `-G`, interpret blame responsibly, and run a complete manual bisect.
