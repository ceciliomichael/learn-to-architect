# Quiz Answers: Synchronization and the Race Detector

1. A clearly stated invariant across all related reads and writes.
2. No. Store it with the protected data and use a pointer receiver.
3. No. It only coordinates completion.
4. No. Only executed paths were observed.
5. When workers can return independent results and one goroutine can combine them clearly.
