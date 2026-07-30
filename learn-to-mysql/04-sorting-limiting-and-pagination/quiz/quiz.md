# Module 04 Quiz

1. In MySQL alternative limit syntax `LIMIT 30, 10`, what does the number `30` represent?
   - A) The number of rows to return.
   - B) The number of rows to skip (offset).
   - C) The primary key ID filter.
   - D) The database port.

2. Why must `ORDER BY` be specified when paginating with `LIMIT`?
   - A) MySQL refuses to execute `LIMIT` without `ORDER BY`.
   - B) Without sorting, row ordering is non-deterministic and pagination results may duplicate or miss rows across pages.
   - C) `ORDER BY` creates a temporary table in memory.
   - D) `ORDER BY` forces strict typing.
