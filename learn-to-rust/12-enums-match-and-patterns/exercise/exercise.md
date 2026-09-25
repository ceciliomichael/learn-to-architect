# Exercises: Module 12

Use a local Cargo project. Predict first.

## 1. Trace

For enum Message { Quit, Text(String), Move { x: i32, y: i32 } }, identify what data each variant carries.

## 2. Repair

Write a match over four variants but handle only three. Use the compiler message to add the missing case rather than a meaningless catch-all.

## 3. Modify

Add Paused to JobState and update describe deliberately.

## 4. Build

Model a download as Waiting, Downloading { received, total }, Failed { reason }, or Finished. Write a function producing a human-readable status.

Finish with cargo fmt, cargo clippy, and cargo check.
