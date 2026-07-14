# Quiz Answers: Goroutines and Lifetimes

1. It schedules a function call to run as a new goroutine and lets the caller continue.
2. No. Correctness cannot depend on a chosen schedule.
3. Before starting the goroutine being counted.
4. `Done` exactly once.
5. No. It only waits for counted work.
