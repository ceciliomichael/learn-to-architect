# Module 05 Exercise Solution

```sql
CREATE TABLE `invoices` (
  `invoice_id` INT AUTO_INCREMENT PRIMARY KEY,
  `client_name` VARCHAR(100) NOT NULL,
  `amount` DECIMAL(12,2) NOT NULL,
  `status` ENUM('pending', 'paid', 'cancelled') DEFAULT 'pending',
  `issued_at` DATETIME DEFAULT CURRENT_TIMESTAMP
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

INSERT INTO `invoices` (`client_name`, `amount`, `status`) VALUES
  ('Acme Corp', 1450.50, 'paid'),
  ('Globex Ltd', 890.00, 'pending');
```

## Explanation

1. `DECIMAL(12,2)` guarantees exact 2 decimal place precision up to 10 integer digits.
2. `ENUM` restricts `status` to only `'pending'`, `'paid'`, or `'cancelled'`.
