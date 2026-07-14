# Exercise: Select and store borrowed text

1. Write `shorter<'a>(left: &'a str, right: &'a str) -> &'a str`.
2. Define `Snippet<'a>` with a `text: &'a str` field.
3. Add a `word_count(&self) -> usize` method.
4. In `main`, select the shorter of two owned strings and store it in a `Snippet`.
5. Print the selected text and count while both owned strings are still alive.
