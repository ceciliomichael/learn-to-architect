# Quiz Answers: Module 32

## 1

It permits a limited set of operations whose safety the compiler cannot fully verify; it does not turn off Rust's rules globally.

## 2

A condition that must hold to avoid invalid memory behavior or other undefined behavior.

## 3

It minimizes the manually audited proof boundary and keeps more code under compiler guarantees.

## 4

No. Tests sample executions and cannot establish every undefined-behavior condition across all inputs and optimizations.

## 5

Guarantee or validate every safety obligation so safe callers cannot trigger undefined behavior through the wrapper.
