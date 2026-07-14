# Module 26: Configuration, Aliases, and Attributes

## What you will learn

You will inspect configuration sources, choose the correct scope, create readable aliases, and use attributes for consistent path handling.

## Configuration scopes

Git reads configuration from several scopes. Common ones are:

- System: settings for users on the machine
- Global: settings for your user account
- Local: settings for one repository
- Worktree: settings for one linked worktree when enabled

More specific settings can override broader ones. Inspect effective values and their sources:

```text
git config --list --show-origin --show-scope
```

Read one value:

```text
git config --get user.name
```

Set a repository-only value:

```text
git config --local core.editor "EDITOR_COMMAND"
```

Remove it from that scope:

```text
git config --local --unset core.editor
```

Do not copy an editor command until you know how that editor waits for files to close.

## Useful aliases

An alias gives a shorter name to a Git subcommand:

```text
git config --global alias.graph "log --graph --oneline --decorate --all"
git graph
```

Aliases can improve a repeated view, but course and team documentation should still show standard commands. Avoid aliases that hide destructive options or make a dangerous action look harmless.

List defined aliases:

```text
git config --get-regexp "^alias\."
```

## Attributes describe path behavior

`.gitattributes` is a tracked file that assigns attributes to matching paths. It can guide line-ending normalization, diff behavior, merge drivers, export rules, and filters.

A simple cross-platform starting point is:

```text
* text=auto
*.sh text eol=lf
*.png binary
```

- `text=auto` lets Git detect text and normalize line endings in repository storage.
- `eol=lf` asks for LF line endings in the working tree for matching paths.
- `binary` is a macro that marks the path as non-text and disables normal text diff and merge behavior.

Choose rules that match project needs. Changing normalization in an existing repository can make many files appear modified and should be a separate reviewed change.

## Inspect attributes

```text
git check-attr -a -- script.sh
git check-attr text eol -- script.sh
```

This explains the effective attributes for the path.

## Ignore and attributes solve different problems

`.gitignore` controls which untracked paths Git normally offers for addition. `.gitattributes` controls how paths are treated after selection and storage. A path can match both, but the files have different jobs.

## Common mistakes

### Changing global config for one project

Use local scope when only one repository needs the setting.

### Creating private aliases in shared scripts

Other machines may not have them. Use standard Git commands in automation.

### Adding attributes without reviewing the resulting diff

Line normalization can affect many paths. Test it in a clean branch and inspect every change.

## Check your understanding

You are ready when you can find where a setting came from, choose local or global scope, and explain the separate purpose of `.gitattributes`.
