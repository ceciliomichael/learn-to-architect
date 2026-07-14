# Exercise: Await two timed tasks

Create a Cargo project and add Tokio with `rt-multi-thread`, `macros`, and `time`.

1. Write `async fn delayed_value(value: u32, millis: u64) -> u32`.
2. Sleep with `tokio::time::sleep`, then return the value.
3. Start two calls together with `tokio::join!`.
4. Put the whole joined operation inside a one-second timeout.
5. Print the sum on success and a clear timeout message on failure.
