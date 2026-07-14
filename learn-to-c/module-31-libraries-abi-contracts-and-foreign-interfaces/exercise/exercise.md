# Exercise: Libraries, ABI Contracts, and Foreign Interfaces

## Steps

1. Export arithmetic_multiply using int32_t parameters and result.
2. Use an extern C guard.
3. Build its object into a static archive.
4. Link a separate client.
5. Document that accepted operands must multiply without int32_t overflow.

## Success check

One header states the interface, one object defines it, the archive links into a separate client, and the documented example prints 42.

