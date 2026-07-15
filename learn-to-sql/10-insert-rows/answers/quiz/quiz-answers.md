# Quiz Answers: Insert Rows

1. It makes the intended mapping clear and avoids dependence on table column order.
2. SQLite assigns an unused integer row identifier for the omitted alias column.
3. Values from rows changed by the statement, using SQLite's supported syntax.
4. No. The statement fails atomically under the normal abort behavior.
5. A failure may reveal invalid data or a wrong assumption that must be understood.
