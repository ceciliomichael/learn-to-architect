# Quiz Answers: Update and Delete Rows Safely

1. Confirm the database, start a transaction when appropriate, and preview with a matching `SELECT`.
2. Every row in the table is updated.
3. It prevents deleting the row if its important state changed since the preview.
4. It undoes changes made since the transaction began.
5. The number of rows changed by the immediately previous insert, update, or delete on that connection.
