# Checkpoint Project C: Multi-Module CLI Application

## Goal

Build a tested notes application with a library crate and a binary entry point. Persistence arrives in the next phase.

## Commands

Support a simple interactive command format:

- add TITLE BODY
- list
- find WORD
- remove INDEX
- stats
- quit

Manual parsing is acceptable here. A production CLI crate is introduced later.

## Suggested structure

~~~text
src/
  lib.rs
  main.rs
  note.rs
  store.rs
tests/
  public_api.rs
~~~

Organize by responsibility rather than blindly following file count.

## Requirements

Use:

- Vec for ordered notes;
- HashMap or HashSet only if it solves a genuine lookup or uniqueness need;
- structs for note data;
- an enum for command or state alternatives;
- Result for invalid operations with useful reasons;
- Option for normal absence;
- unit tests for domain rules;
- integration tests for the public library API.

Use generics or traits only when a real reusable contract exists.

## External dependency rule

You may add one small external crate if it solves a real requirement. If you do, add DEPENDENCY_REVIEW.md containing:

1. why the standard library is insufficient;
2. which crate API you use;
3. enabled features;
4. a summary of cargo tree;
5. what would change if the dependency were removed.

## Quality gate

~~~text
cargo fmt --check
cargo clippy --all-targets --all-features
cargo test
cargo check
~~~

Understand every diagnostic.

## Architecture reflection

Draw and explain:

~~~text
terminal input
    |
    v
binary coordination
    |
    v
public library API
    |
    v
domain/store logic
~~~

The lower domain layer should not need to know how terminal text is displayed.

Continue to [Module 24](../../24-files-paths-and-streamed-io/README.md).
