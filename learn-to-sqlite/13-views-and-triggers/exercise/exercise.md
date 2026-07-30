# Module 13 Exercise

1. Create a View named `low_stock_items` that selects items from `inventory` where `price < 20.0`.
2. Create an audit table `price_changes` (`id` INT PRIMARY KEY, `item_id` INT, `old_price` REAL, `new_price` REAL).
3. Create an `AFTER UPDATE OF price ON inventory` trigger that records old and new prices into `price_changes`.
