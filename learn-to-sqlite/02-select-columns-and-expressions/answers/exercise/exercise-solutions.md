# Module 02 Exercise Solution

## SQL Query

```sql
SELECT 
  'Item: ' || name AS item_description,
  price AS unit_price,
  price * 0.90 AS sale_price
FROM items;
```

### Expected Output

```text
┌────────────────────┬────────────┬────────────┐
│  item_description  │ unit_price │ sale_price │
├────────────────────┼────────────┼────────────┤
│ Item: Notebook     │ 4.5        │ 4.05       │
│ Item: Fountain Pen │ 12.0       │ 10.8       │
└────────────────────┴────────────┴────────────┘
```

## Explanation

1. `'Item: ' || name` joins the text literal `'Item: '` with the `name` column using SQLite's string concatenation operator (`||`).
2. `AS item_description` aliases the concatenated expression so the header prints clearly.
3. `price * 0.90 AS sale_price` calculates 90% of the `price` column for each row dynamically without altering disk storage.
