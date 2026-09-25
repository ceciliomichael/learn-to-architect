# Exercise Solutions: Module 24

Attempt the exercises before reading.

## 1. Trace

Streaming can process each line and release its temporary memory rather than allocating space for the entire file.

## 2. Repair

Return io::Result from the lower-level function and decide how to present the error in main.

## 3. Modify

Keep a counter and inspect each line after propagating per-line read errors. No full-file allocation is needed.

## 4. Build

Separate a function that classifies/counts an iterator of text from the function that opens the file. This isolates domain logic from filesystem failure.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
