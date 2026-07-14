# Quiz answers

1. One owner controls a heap-allocated value.
2. No. It increments the strong reference count.
3. Its reference count is not synchronized for cross-thread access.
4. The values may never reach a strong count of zero, causing a memory leak.
5. Use it for a non-owning link that should not keep the value alive.
