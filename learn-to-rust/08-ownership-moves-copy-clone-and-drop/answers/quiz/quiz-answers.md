# Quiz Answers: Module 08

## 1

String owns a resource that must not be cleaned up twice, so ordinary assignment transfers ownership rather than duplicating that resource implicitly.

## 2

The value can be duplicated implicitly and both bindings remain usable because that duplication is defined as safe and appropriate for the type.

## 3

Cloning can have cost and semantic meaning, so Rust makes the request visible.

## 4

Rust runs Drop behavior for the owned value, releasing resources according to its type.

## 5

Ownership is a language-level responsibility model. Compiler layout and optimization decisions are separate implementation details.
