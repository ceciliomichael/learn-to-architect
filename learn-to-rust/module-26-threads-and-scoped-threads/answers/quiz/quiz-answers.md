# Quiz answers

1. It returns a `JoinHandle`.
2. The thread may outlive the current scope, so it must own captured data rather than borrow short-lived values.
3. Every scoped thread is joined before the scope returns.
4. It returns `Err` with the panic payload.
5. The program would lose the worker's result and its direct panic report.
