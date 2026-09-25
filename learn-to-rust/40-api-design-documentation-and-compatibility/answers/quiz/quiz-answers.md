# Quiz Answers: Module 40

## 1

External code may depend on public items and their behavior, so public design creates compatibility obligations.

## 2

A newtype creates a distinct compiler-recognized type with its own construction and methods. A type alias is another name for the same underlying type.

## 3

Callers cannot bypass validation or mutate representation arbitrarily, so invariant-preserving operations remain under the type's control.

## 4

They can compile and run as documentation tests, reducing drift between examples and the actual API.

## 5

No. Behavior, errors, output formats, side effects, ordering, and operational expectations can also be contracts.

## 6

When callers need to understand the circumstances of failure to use or recover from the API correctly.

## 7

Downstream code may use exhaustive matches and therefore needs a new branch.

## 8

No. Debug is developer-oriented and not intended as a stable serialization format.

## 9

The caller may mutate the value without going through operations that enforce the containing type's rules.

## 10

No. Expose abstractions when the current contract benefits from them. Hypothetical flexibility has real maintenance cost.
