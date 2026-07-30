# Module 02 Exercise

1. Open `bookstore.db` using `sqlite3`.
2. Query the `items` table and return:
   - Item name in uppercase description format: `'Item: ' || name` aliased as `item_description`
   - Unit price aliased as `unit_price`
   - Discounted price (10% off: `price * 0.90`) aliased as `sale_price`
