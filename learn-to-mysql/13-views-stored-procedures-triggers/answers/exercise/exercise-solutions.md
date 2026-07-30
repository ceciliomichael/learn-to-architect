# Module 13 Exercise Solution

```sql
DELIMITER //

CREATE PROCEDURE `GetProductCount`(OUT `p_count` INT)
BEGIN
  SELECT COUNT(*) INTO `p_count` FROM `items`;
END //

DELIMITER ;

CALL GetProductCount(@total_products);
SELECT @total_products;
```

### Expected Output

```text
+-----------------+
| @total_products |
+-----------------+
|               2 |
+-----------------+
```

## Explanation

1. `DELIMITER //` temporarily changes the CLI end-of-statement character.
2. `CALL GetProductCount(@total_products)` populates the user session variable `@total_products`.
