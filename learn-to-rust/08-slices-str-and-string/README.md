# Module 08: Slices, str, and String

## What you will learn

You will borrow consecutive data with slices and handle UTF-8 strings without invalid indexing.

```rust
fn first_word(text: &str) -> &str {
    match text.find(' ') {
        Some(index) => &text[..index],
        None => text,
    }
}

fn main() {
    let owned = String::from("clear Rust");
    println!("{}", first_word(&owned));
}
```

`String` owns growable UTF-8 data. `&str` borrows valid UTF-8 text and is usually the best read-only parameter. String literals have type `&'static str` because their bytes live for the program.

Rust rejects `text[0]` because UTF-8 characters use varying bytes and indexing would have unclear meaning. Iterate with `.bytes()` for encoded bytes or `.chars()` for Unicode scalar values. Human-visible graphemes require a suitable reviewed library.

String slicing uses byte offsets and panics if a boundary is not valid UTF-8. Prefer methods that find or produce valid boundaries for you.

`&[T]` borrows consecutive array or vector elements. `&mut [T]` permits exclusive element mutation without taking ownership of the collection.

## Check your understanding

You are ready when you can choose `String`, `&str`, bytes, chars, or a general slice from the needed ownership and meaning.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
