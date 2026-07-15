# Exercises: Goroutines and Lifetimes

1. Start four workers that print distinct labels and wait for all of them.
2. Run several times and observe that order is not a contract.
3. Pass every loop value as a worker argument.
4. Remove `Wait`, observe possible early exit, then restore it.
5. Explain why `WaitGroup` does not protect a shared map.
