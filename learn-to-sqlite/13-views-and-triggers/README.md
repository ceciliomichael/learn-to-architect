# Module 13: Store Reusable Queries with Views and Automate with Triggers

## What You Will Learn

In this module, you will learn how to encapsulate complex queries into virtual tables called **Views** (`CREATE VIEW`), and how to automate background audit logging and validation using **Triggers** (`CREATE TRIGGER`).

---

## Views (`CREATE VIEW`)

A View is a stored query that acts like a read-only virtual table. It does not store physical data itself; instead, it executes its underlying query dynamically whenever queried.

```sql
CREATE VIEW active_customer_orders AS
SELECT c.name, o.id AS order_id, o.amount
FROM customers c
JOIN orders o ON c.id = o.customer_id
WHERE o.amount > 0;

-- Query the view just like a table:
SELECT * FROM active_customer_orders WHERE amount > 100.0;
```

---

## Triggers (`CREATE TRIGGER`)

A Trigger is a set of SQL statements that automatically execute when a specific data modification event (`INSERT`, `UPDATE`, or `DELETE`) occurs on a table.

Inside a trigger:
- `NEW.column`: Refers to the new row being inserted or updated.
- `OLD.column`: Refers to the existing row being updated or deleted.

```sql
CREATE TABLE audit_log (
  log_id INTEGER PRIMARY KEY AUTOINCREMENT,
  action TEXT,
  emp_id INT,
  timestamp DATETIME DEFAULT CURRENT_TIMESTAMP
);

CREATE TRIGGER log_emp_delete 
AFTER DELETE ON employees
FOR EACH ROW
BEGIN
  INSERT INTO audit_log (action, emp_id) VALUES ('DELETE', OLD.emp_id);
END;
```

---

## Check Your Understanding

1. What is the difference between physical table data and data presented by a View?
2. What do `OLD` and `NEW` refer to inside a SQLite trigger block?
