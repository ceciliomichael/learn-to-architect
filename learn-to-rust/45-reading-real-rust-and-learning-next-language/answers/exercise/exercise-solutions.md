# Exercise Solutions: Module 45

These exercises depend on the repository and second language you choose, so there is no universal source-code solution.

## 1. Codebase reconnaissance

A strong report uses evidence from:

- Cargo.toml;
- Cargo.lock;
- crate roots;
- cargo metadata;
- cargo tree;
- tests;
- build and release configuration.

It clearly separates observed facts from assumptions.

## 2. Trace one behavior

A good trace follows one real vertical slice and names the actual types, functions, and external boundaries.

It does not attempt to summarize the entire repository.

## 3. Read from signatures

Useful predictions include observations such as:

- by-value ownership transfer;
- shared borrow;
- mutable borrow;
- Option for normal absence;
- Result for recoverable failure;
- trait bounds;
- Arc or synchronization;
- async Future behavior.

The implementation may reveal more, but the signature should already tell you a surprising amount.

## 4. Create a language transfer map

UNKNOWN is better than invented information.

The exercise succeeds when your investigation becomes a checklist of semantic questions rather than a list of syntax substitutions.

## 5. Rebuild a known project

A strong comparison recognizes that parsing, validation, decomposition, errors, collections, testing, and boundary design still exist while syntax, runtime behavior, ownership enforcement, and ecosystem tools change.

Do not judge the new language by how closely it resembles Rust.
