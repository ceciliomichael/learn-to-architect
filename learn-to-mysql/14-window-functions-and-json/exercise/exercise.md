# Module 14 Exercise

1. Create table `events` (`id` INT AUTO_INCREMENT PRIMARY KEY, `payload` JSON).
2. Insert 1 row with `{"event_type": "login", "user_id": 42}`.
3. Query `events` and extract `event_type` using `->>`.
