# Exercises: Module 25

Work locally and explain your choices.

## 1. Trace

If serde_json successfully parses refresh_seconds = 999999, is the Settings value automatically valid for the domain?

## 2. Repair

Replace unwrap around from_str with explicit Result propagation or handling.

## 3. Modify

Add a theme enum with two allowed variants and derive Serde for it.

## 4. Build

Define a SavedProject format with version, name, and entries. Parse JSON, validate non-empty name and bounded entry count, and reject unsupported format versions.

Finish with cargo fmt, cargo clippy, cargo test when tests exist, and cargo check.
