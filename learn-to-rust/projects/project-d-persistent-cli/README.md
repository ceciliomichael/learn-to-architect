# Checkpoint Project D: Persistent CLI Tool

## Goal

Turn the notes domain from Checkpoint C into a persistent command-line application.

Use the ecosystem intentionally:

- Clap for the CLI;
- Serde and serde_json for persistence;
- tracing and tracing-subscriber for diagnostics.

## Required commands

~~~text
notes add TITLE BODY
notes list
notes find WORD
notes remove INDEX
notes stats
~~~

Provide a configurable data-file path. Define and document precedence among:

1. explicit CLI option;
2. environment variable;
3. application default.

## Persistence requirements

Store a versioned JSON document rather than serializing an unversioned raw Vec forever.

Example conceptual shape:

~~~json
{
  "format_version": 1,
  "notes": []
}
~~~

On load:

- enforce a reasonable file size before parsing when practical;
- handle missing file according to a documented first-run policy;
- return malformed JSON as a controlled error;
- reject unsupported format versions;
- validate domain fields after deserialization.

On save, avoid casually truncating the only known-good copy before the replacement data is ready. Research the guarantees your target platform provides for temporary files, flush behavior, rename/replace, and crash durability before claiming a save is atomic or durable.

## Layering target

~~~text
CLI / environment
       |
       v
application orchestration
       |
       +---- diagnostics
       |
       v
domain library
       |
       v
persistence adapter
       |
       v
filesystem + JSON
~~~

Domain note rules should not depend on Clap, tracing, or serde_json parsing details.

## Tests

At minimum:

- unit tests for domain rules;
- integration tests for the public library;
- persistence round-trip test using an isolated temporary directory strategy;
- invalid JSON test;
- unsupported-version test;
- configuration precedence test.

## Quality gate

~~~text
cargo fmt --check
cargo clippy --all-targets --all-features
cargo test
cargo check
~~~

Also run cargo tree and explain your direct dependencies and major transitive groups.

Continue to [Module 28](../../28-smart-pointers-box-rc-arc/README.md).
