# Module 10: Strings, str, and Slices

## Outcome

Choose between owned String and borrowed str, use slices as views into existing data, and reason correctly about UTF-8 text.

## Why this matters

Text is one of the most common data forms, but text is not the same thing as an array of one-byte characters. Rust makes ownership and encoding visible so text APIs cannot casually produce invalid character boundaries.

## Programming concept

A slice is a borrowed view into a contiguous region of another collection. Text encoding maps characters to bytes. UTF-8 uses a variable number of bytes for many characters, so byte positions and human-perceived character positions are not interchangeable.

## Rust model

String is owned, growable UTF-8 text. str is the string-slice type and is normally used behind a reference as &str. String literals are &str values embedded in the program. &[T] is a slice of elements. String byte slicing is allowed only at valid UTF-8 boundaries, and direct numeric string indexing is not supported.

## Local Cargo example

~~~text
cargo new strings_and_slices --edition 2024
cd strings_and_slices
~~~

Replace src/main.rs:

~~~rust
fn first_word(text: &str) -> &str {
    match text.find(' ') {
        Some(index) => &text[..index],
        None => text,
    }
}

fn main() {
    let owned = String::from("Rust makes ownership visible");
    let word = first_word(&owned);

    println!("first: {word}");
    println!("bytes: {}", owned.len());

    for ch in "Rustacean".chars() {
        print!("{ch} ");
    }
    println!();
}
~~~

Run cargo check, cargo run, and cargo fmt.



## Walkthrough

- first_word borrows text and returns a slice into the same text.
- find returns a byte index that is valid for the matched ASCII space boundary.
- &text[..index] does not allocate a new String.
- len on strings reports bytes, not Unicode character count.
- chars iterates Unicode scalar values rather than raw bytes.

## Deliberate mistake

~~~rust
fn main() {
    let text = String::from("é");
    println!("{}", text[0]);
}
~~~

Rust does not support numeric indexing into strings because an arbitrary byte position may be inside a multi-byte UTF-8 sequence and because the intended unit could be byte, Unicode scalar value, or grapheme cluster.

Corrected version:

~~~rust
fn main() {
    let text = String::from("é");
    println!("first char: {:?}", text.chars().next());
    println!("bytes: {:?}", text.as_bytes());
}
~~~

## Mental model

- Use String when your code needs ownership or growth.
- Use &str for borrowed text input when ownership is unnecessary.
- A string's byte length is not necessarily its character count.
- Slices borrow existing data instead of copying it.
- Choose the text unit your problem actually needs: bytes, Unicode scalar values, or user-perceived grapheme clusters.

## Common mistakes

- Accepting &String when &str is sufficient.
- Assuming len means character count.
- Slicing text at arbitrary numeric byte offsets.
- Calling clone to obtain a substring when a borrow is enough.
- Treating Unicode as an edge case that can be ignored in user-facing text.

## Transfer to other languages

Owned strings, immutable string views, byte encodings, and Unicode handling differ by language, but every text system has an encoding and every API must choose what a position or length means.

## Guided practice

1. Create a String and pass it to a function taking &str.
2. Take a slice of an integer array.
3. Compare byte length and chars count for ASCII and non-ASCII text.
4. Print bytes and chars separately for the same text.

## Exercise and quiz

Complete [the exercises](exercise/exercise.md) and [the quiz](quiz/quiz.md) before reading the answers.

## Readiness check

- distinguish String, str, and &str;
- explain what a slice borrows;
- state that String len is a byte count;
- avoid arbitrary numeric string indexing.

## Next

Continue to [Module 11](../11-structs-and-methods/README.md).
