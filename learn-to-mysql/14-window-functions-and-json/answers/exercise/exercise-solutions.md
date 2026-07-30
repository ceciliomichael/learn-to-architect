# Module 14 Exercise Solution

```sql
CREATE TABLE `events` (
  `id` INT AUTO_INCREMENT PRIMARY KEY,
  `payload` JSON NOT NULL
) ENGINE=InnoDB;

INSERT INTO `events` (`payload`) VALUES ('{"event_type": "login", "user_id": 42}');

SELECT `id`, `payload`->>'$.event_type' AS `event_type`
FROM `events`;
```

### Expected Output

```text
+----+------------+
| id | event_type |
+----+------------+
|  1 | login      |
+----+------------+
```

## Explanation

1. `payload` column of type `JSON` enforces valid JSON syntax on insertion.
2. `payload->>'$.event_type'` unquotes the scalar value `'login'`.
