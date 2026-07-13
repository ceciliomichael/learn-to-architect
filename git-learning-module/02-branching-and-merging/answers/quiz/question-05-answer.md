# Answer to Question 05

**Viewing all existing branches and identifying the current one.**

To view a comprehensive list of all local branches within your repository, you execute the base command:

```bash
git branch
```

When this command is run without any flags or arguments, the terminal will output a vertical list of branch names.

Git explicitly indicates your currently active branch (the universe you are currently standing inside) by placing a literal asterisk character (`*`) immediately to the left of the branch name. Additionally, depending on terminal configuration, the active branch name is frequently highlighted in a distinct color, typically green.

Example output:
```text
  feature-auth
* main
  hotfix-database
```
In this scenario, the engineer is currently operating securely within the `main` timeline.
