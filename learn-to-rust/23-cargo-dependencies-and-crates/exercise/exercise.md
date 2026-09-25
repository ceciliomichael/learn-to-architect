# Exercises: Module 23

Work locally and explain your choices.

## 1. Trace

Cargo.toml lists one direct dependency but cargo tree shows twelve packages. Why?

## 2. Repair

In a disposable project, add an unnecessary crate, inspect cargo tree, remove the crate, and identify which graph nodes disappear.

## 3. Modify

Add unicode-segmentation and state precisely why its grapheme API solves a requirement that bytes or chars alone do not.

## 4. Build

Write DEPENDENCY_REVIEW.md for one small crate. Record purpose, API used, features, transitive impact, verifiable license metadata, maintenance signals to check, risks, and how you would remove it.

Finish with cargo fmt, cargo clippy, cargo test when tests exist, and cargo check.
