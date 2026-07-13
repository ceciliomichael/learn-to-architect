# Answer to Question 04

**Describe conflict markers and the resolution process.**

When a merge conflict occurs, Git halts the automatic fusion process and edits the conflicting files directly, injecting standard syntax markers to explicitly bracket the contradictory code blocks.

The structure is as follows:
1. `<<<<<<< HEAD`: This specific string signifies the top boundary of the conflict. The code immediately following this line belongs to your active, current branch (the destination).
2. `=======`: This serves as the absolute dividing line. It separates the conflicting code of the destination branch from the incoming branch.
3. `>>>>>>> [branch-name]`: This string signifies the bottom boundary of the conflict, displaying the name of the incoming branch being merged. The code immediately preceding this line belongs to that incoming branch.

**The Exhaustive Resolution Process:**
1. Open the compromised file in a code editor.
2. Analyze the divergent logic bracketed by the conflict markers.
3. Make an executive engineering decision on the correct final state of the file. You may choose the `HEAD` code, the incoming code, or write entirely new logic that combines aspects of both.
4. Manually and precisely delete the Git marker text (`<<<<<<<`, `=======`, `>>>>>>>`). The presence of these markers in a saved file will often cause compilation failures.
5. Save the structurally correct file.
6. Tell Git the human intervention is complete by staging the file using `git add <filename>`.
7. Conclude the operation by executing `git commit`. Git will automatically populate the commit message with a standard merge resolution template.
