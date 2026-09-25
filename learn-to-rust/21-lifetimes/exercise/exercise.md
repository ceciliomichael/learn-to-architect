# Exercises: Module 21

Work locally and explain your choices.

## 1. Trace

Can a reference returned by longer safely remain usable after one of the possible input referents is destroyed?

## 2. Repair

Attempt to return &str referring to a local String, then return String by value instead.

## 3. Modify

Create Excerpt<'a> holding part: &'a str and construct it from a String owned by main.

## 4. Build

Write choose_non_empty<'a>(first: &'a str, second: &'a str) -> Option<&'a str> and explain the annotation in plain English.

Finish with cargo fmt, cargo clippy, cargo test when tests exist, and cargo check.
