# Module 13: Views, Stored Procedures, and Triggers

## What You Will Learn

In this module, you will learn how to encapsulate reusable queries in Views (`CREATE VIEW`), create parameter-driven server-side business logic using Stored Procedures (`CREATE PROCEDURE`, `DELIMITER //`), and construct automated triggers (`CREATE TRIGGER`).

---

## Views in MySQL

```sql
CREATE VIEW `v_high_value_orders` AS
SELECT c.`name` AS `customer`, o.`id` AS `order_id`, o.`amount`
FROM `customers` c
JOIN `orders` o ON c.`id` = o.`customer_id`
WHERE o.`amount` > 500.00;
```

---

## Stored Procedures (`DELIMITER //`)

Because procedural code blocks contain multiple semicolons, change the CLI delimiter before creating stored procedures:

```sql
DELIMITER //

CREATE PROCEDURE `GetCustomerBalance`(
  IN `p_customer_id` INT,
  OUT `p_total_balance` DECIMAL(10,2)
)
BEGIN
  SELECT SUM(`amount`) INTO `p_total_balance`
  FROM `orders`
  WHERE `customer_id` = `p_customer_id`;
END //

DELIMITER ;

-- Calling a procedure:
CALL GetCustomerBalance(1, @balance);
SELECT @balance;
```

---

## Triggers in MySQL

```sql
DELIMITER //

CREATE TRIGGER `before_employee_insert`
BEFORE INSERT ON `employees`
FOR EACH ROW
BEGIN
  IF NEW.`salary` < 30000.00 THEN
    SIGNAL SQLSTATE '45000'
    SET MESSAGE_TEXT = 'Salary below minimum wage requirement';
  END IF;
END //

DELIMITER ;
```

---

## Check Your Understanding

1. Why must you use `DELIMITER //` when defining stored procedures or triggers in the MySQL CLI?
2. What does `SIGNAL SQLSTATE '45000'` do inside a MySQL trigger?
