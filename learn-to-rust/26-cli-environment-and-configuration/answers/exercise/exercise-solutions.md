# Exercise Solutions: Module 26

Attempt the exercises before reading.

## 1. Trace

Automation may treat stdout as structured or expected program output, so extra diagnostic text corrupts that interface.

## 2. Repair

Use checked iteration for a learning parser or Clap for a real interface so missing/invalid arguments become deliberate errors and help.

## 3. Modify

Add a bool field with arg(long) and another Subcommand variant. Keep business action separate from parser details.

## 4. Build

Resolve CLI first, then environment, then default, or another explicitly documented order. Test each combination without reading real process state inside the pure resolution function.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
