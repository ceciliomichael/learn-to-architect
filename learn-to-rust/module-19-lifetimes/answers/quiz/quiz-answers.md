# Quiz answers

1. No. It only describes relationships that Rust must verify.
2. The result is borrowed from one of the inputs and cannot outlive either input's shared valid period.
3. The compiler must know that the struct cannot outlive the value referenced by its field.
4. A string literal is a common example.
5. Returning an owned value is often simpler and safer.
