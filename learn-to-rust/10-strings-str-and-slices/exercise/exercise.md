# Exercises: Module 10

Use a local Cargo project. Predict first.

## 1. Trace

For the text café, explain why byte length and chars count may differ.

## 2. Repair

Try text[0] on a String and replace it with an operation that explicitly asks for the first char.

## 3. Modify

Change first_word to return the whole input when there is no space and verify no new String is allocated.

## 4. Build

Build a text_stats function taking &str and returning a tuple containing byte count, char count, and first char as Option<char>.

Finish with cargo fmt, cargo clippy, and cargo check.
