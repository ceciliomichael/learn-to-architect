# Answer: Question 04  -  The 300-Line Rule

---

## What is the 300-line rule?

The **300-line rule** is a practical heuristic: any logic file that approaches 300 lines is almost certainly doing too many things at once. Before a file crosses that threshold, stop and deliberately identify its distinct responsibilities, then split them into separate files.

The rule **does not apply** to purely declarative files such as type definitions, JSON configuration, or generated code  -  those can legitimately be long without indicating a design problem.

---

## Why is it a useful heuristic?

### 1. Lines of code correlate with number of responsibilities

A focused file with a single responsibility  -  say, a repository that reads and writes one entity  -  rarely exceeds 100 - 150 lines. When a file approaches 300 lines, it is almost always because it has accumulated a second, third, or fourth responsibility over time. The line count is a **visible symptom** of an invisible architectural problem.

### 2. It forces the conversation early

Left unchecked, files grow incrementally. No single addition feels large enough to warrant splitting. The 300-line rule creates a **fixed checkpoint** that interrupts the "just one more function" pattern and forces a deliberate review before the file becomes a God Object.

### 3. It keeps files humanly navigable

A developer reading a 50-line service can hold its entire logic in working memory. A developer opening a 600-line file must scroll extensively, mentally track multiple unrelated concerns, and risks missing interactions between functions. Files under 300 lines are fast to read, reason about, and modify confidently.

### 4. It protects testability

Smaller, focused files are easier to test in isolation. A 300-line file mixing data access, validation, and orchestration forces test setup to account for all three concerns simultaneously. Splitting the file makes each unit independently testable with minimal mocking.

---

## What does a file approaching 300 lines often indicate?

A file approaching 300 lines typically signals one or more of these problems
| Signal | What it means |
|---|---|
| Multiple unrelated functions | Two or more features have been placed in one file instead of separate modules. |
| Mixed layers | Data access, business rules, and orchestration have been written in the same place. |
| A "God Object" forming | One file is accumulating knowledge it does not need to own. |
| Missing abstractions | Logic that should be extracted into a helper, service, or utility is being written inline instead. |
| Vague file name | The file is named something broad like `utils.ts` or `helpers.ts`  -  a sign it has no clear responsibility boundary. |

### The right response

When a file is growing toward 300 lines
1. List every distinct responsibility you can find in the file.
2. Create a new file for each responsibility.
3. Move the relevant code into its dedicated file.
4. Update imports.

The entry point or orchestrator keeps only the code that wires the pieces together.

---

## Summary

The 300-line rule is not about the number itself  -  it is about using a concrete, measurable threshold to enforce the Single Responsibility Principle before a codebase becomes difficult to maintain. A file that is growing is a file that is accumulating responsibilities, and early intervention is always cheaper than a large-scale refactor later.
