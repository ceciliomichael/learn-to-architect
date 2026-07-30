# Module 05 Exercise

1. Create a MySQL table `invoices` with:
   - `invoice_id` INT AUTO_INCREMENT PRIMARY KEY
   - `client_name` VARCHAR(100) NOT NULL
   - `amount` DECIMAL(12,2) NOT NULL
   - `status` ENUM('pending', 'paid', 'cancelled') DEFAULT 'pending'
   - `issued_at` DATETIME DEFAULT CURRENT_TIMESTAMP
   - `ENGINE=InnoDB DEFAULT CHARSET=utf8mb4`
2. Insert 2 valid invoice rows.
