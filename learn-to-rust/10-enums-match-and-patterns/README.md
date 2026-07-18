# Module 10: Enums, Match, and Patterns

## What you will learn

You will represent a value that is exactly one of several states and handle every state explicitly.

```rust
enum Message {
    Quit,
    Text(String),
    Move { x: i32, y: i32 },
}

fn describe(message: Message) {
    match message {
        Message::Quit => println!("quit"),
        Message::Text(text) => println!("{text}"),
        Message::Move { x, y } => println!("{x},{y}"),
    }
}
```

Each variant can carry different data. `match` is exhaustive and patterns destructure values. Use `ref`, references in patterns, or match borrowed values when ownership must remain with the caller.

Guards add conditions after a pattern. `if let` handles one interesting variant; `let else` extracts a required pattern and exits otherwise. Prefer full match when several cases carry business meaning.

Enums prevent impossible combinations that several unrelated booleans can create.

## Check your understanding

You are ready when you can list every valid state and prove a match handles all of them.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
