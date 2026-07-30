# Module 13 Exercise Solution

```sql
CREATE VIEW low_stock_items AS
SELECT * FROM inventory WHERE price < 20.0;

CREATE TABLE price_changes (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  item_id INTEGER,
  old_price REAL,
  new_price REAL
);

CREATE TRIGGER track_price_update
AFTER UPDATE OF price ON inventory
FOR EACH ROW
BEGIN
  INSERT INTO price_changes (item_id, old_price, new_price)
  VALUES (OLD.id, OLD.price, NEW.price);
END;

-- Test trigger:
UPDATE inventory SET price = 18.0 WHERE id = 1;
SELECT * FROM price_changes;
```

## Explanation

1. `low_stock_items` provides a dynamic query alias for low-priced inventory.
2. `AFTER UPDATE OF price ON inventory` executes whenever the `price` column is mutated, logging `OLD.price` and `NEW.price`.
