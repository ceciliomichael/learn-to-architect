# Quiz Answers: Module 39

## 1

A module organizes names inside a crate. A crate is a Rust compilation unit. A Cargo package describes one or more crate targets. A workspace coordinates multiple packages.

## 2

No. Cargo features are compile-time capability and dependency configuration.

## 3

Feature resolution can combine requests from multiple users of the same dependency. Additive features can coexist instead of creating contradictory modes.

## 4

No. A member must still opt into the workspace dependency requirement with workspace = true.

## 5

Crates introduce public API, manifest, compilation, dependency, and maintenance boundaries. Those costs should correspond to meaningful package responsibilities.

## 6

It verifies that every workspace member participates successfully in the selected build operation and catches failures in packages you did not explicitly select.

## 7

Otherwise optional code may have accidentally become required even though the package claims a minimal configuration is supported.

## 8

No. Feature unification means the resolved dependency may receive the union of enabled features.

## 9

When the choice is an operational mode, user preference, environment choice, or value that should change without recompilation.

## 10

Responsibilities and desired change direction. Lower-level stable policy should not casually depend on higher-level delivery mechanisms.
