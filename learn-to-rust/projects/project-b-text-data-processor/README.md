# Checkpoint Project B: Text and Data Processor

## Goal

Build a local text-analysis program that forces you to make ownership, borrowing, modeling, optional-value, and error decisions.

The program reads lines from standard input until the user enters quit.

For every non-empty line, report:

- byte length;
- Unicode scalar-value count using chars;
- first word as borrowed text when possible;
- first numeric token if one can be parsed;
- whether a chosen keyword exists.

## Required design

Create a struct named Analysis containing values that should be owned after analysis. Use an enum for at least one meaningful classification such as Empty, Short, Medium, or Long.

Use:

- &str for read-only function inputs when ownership is unnecessary;
- Option for something that may simply be absent;
- Result for something that can fail with a useful reason;
- methods where behavior clearly belongs with a struct;
- match where multiple enum states matter.

Do not use clone only to satisfy the borrow checker. If you clone, explain why two independent owners are required.

## Milestones

1. Analyze one hard-coded String.
2. Extract read-only calculations into borrowed functions.
3. Add a struct for the result.
4. Add an enum classification.
5. Add Option-returning search.
6. Add one Result-returning parser or validator.
7. Add the input loop.
8. Handle invalid data without panic.
9. Run cargo fmt, cargo clippy, and cargo check.

## Ownership review

Draw a small table for one input line:

| Value | Owner | Borrowers | Move/Copy/Clone |
| --- | --- | --- | --- |
| input String | ? | ? | ? |
| first-word view | none, it borrows | ? | ? |
| Analysis | ? | ? | ? |

Fill it from your implementation.

## Test cases

Use ASCII, non-ASCII text, empty input, whitespace-only input, a line containing a number, a line with no number, and a long line.

## Reflection

Explain why a garbage-collected language would still need decisions about mutation, aliases, parsing, absence, and error boundaries even though it would manage memory reclamation differently.

Continue to [Module 15](../../15-vectors-and-dynamic-collections/README.md).
