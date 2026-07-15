# Exercises: Handle Exceptions Deliberately

1. Keep asking for an integer until conversion succeeds, catching only `ValueError`.
2. Write safe division that catches `ZeroDivisionError` at the user-facing boundary.
3. Write a function that raises `ValueError` for a negative quantity.
4. Reject insufficient stock with `ValueError` containing requested and available counts.
5. Convert an internal `KeyError` into a clearer `ValueError` while preserving the cause.
