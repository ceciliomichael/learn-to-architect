# Exercise Solutions: Module 44

## 1. Inspect a release artifact

The exact path and size depend on your system.

A complete answer records the environment and artifact rather than claiming one universal filename or size.

The important distinction is that you execute the already-built release artifact directly during smoke testing.

## 2. Cross-compilation plan

A correct plan does not assume rustup target add is sufficient.

It identifies:

- Rust target components;
- linker;
- platform SDK;
- native libraries;
- build scripts;
- target execution/testing.

Unknown details should be investigated before implementation.

## 3. Package a CLI

A good package includes only files required for distribution and compliance.

Do not include:

- .env;
- credentials;
- development databases;
- shell history;
- unrelated build output.

## 4. Build a release checklist

The checklist should order verification before publication.

Credentials for publishing or signing should be available only to the stage that needs them.

## 5. Rollback analysis

Valid strategies include backward-compatible format evolution, preserving old readable fields, creating a pre-migration backup, or using a staged migration.

The key lesson is that artifact rollback and data rollback are different problems.
