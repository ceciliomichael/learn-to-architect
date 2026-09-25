# Exercises: Module 45

## 1. Codebase reconnaissance

Choose a Rust project you already have locally.

Without reading every source file, create RECON.md containing:

- package or workspace shape;
- entry points;
- top-level modules;
- five important dependencies;
- important features;
- test locations;
- external I/O boundaries;
- concurrency model if any;
- unsafe or FFI areas if any;
- build and release clues.

Mark unknown items as UNKNOWN.

## 2. Trace one behavior

Choose one user-visible behavior.

Write a real trace using actual names from the codebase:

~~~text
input
  |
  v
parser
  |
  v
application operation
  |
  v
domain types
  |
  v
external boundary
  |
  v
result
  |
  v
user output
~~~

Do not document unrelated paths.

## 3. Read from signatures

Choose five function or method signatures.

Before reading implementation, predict what each signature tells you about:

- ownership;
- borrowing;
- optionality;
- failure;
- generic or trait requirements;
- concurrency or async behavior if visible.

Then inspect implementation and correct your notes.

## 4. Create a language transfer map

Choose one language you want to learn next.

Create NEXT_LANGUAGE.md with:

- execution model;
- memory/resource model;
- core values and collection types;
- error model;
- module/package model;
- dependency tool;
- test system;
- concurrency model;
- async model;
- build/release model.

Use UNKNOWN instead of guessing facts you have not verified.

## 5. Rebuild a known project

When you begin learning the next language, rebuild Checkpoint A.

Write a comparison containing:

- concepts that transferred unchanged;
- syntax that changed;
- runtime assumptions that changed;
- Rust habits that did not fit;
- things the new language made easier;
- guarantees that became weaker or stronger.

The goal is comparison, not declaring one language better.
