# Quiz Answers: Module 41

## 1

It describes which components know about and rely on which other components.

## 2

A boundary where a real collaborator can be replaced by controlled behavior for testing or another implementation.

## 3

If the inner function only needs already-resolved values, passing those values is simpler than introducing an abstraction for how they were obtained.

## 4

Near the outside of the application, commonly in main or another composition root.

## 5

Ownership and mutation become implicit, tests interfere with each other more easily, concurrency requires hidden synchronization, and dependencies are harder to see.

## 6

No. Architecture follows the actual problem. Some domains are intrinsically about external protocols or devices. Avoid unnecessary coupling rather than obeying a slogan.

## 7

When it represents useful variation, substitution, a volatile external boundary, or a meaningful public capability.

## 8

It translates between an external mechanism or representation and an internal contract or domain model.

## 9

One component owns mutation, communication is explicit, and synchronization can become a message protocol instead of many shared lock relationships.

## 10

No. Patterns are vocabulary and reusable ideas. Responsibility and dependency quality still require judgment.
