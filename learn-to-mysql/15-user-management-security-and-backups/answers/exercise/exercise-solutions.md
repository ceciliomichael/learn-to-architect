# Module 15 Exercise Solution

```sql
CREATE USER 'read_only_user'@'localhost' IDENTIFIED BY 'Secret123!';
GRANT SELECT ON `store_db`.* TO 'read_only_user'@'localhost';
FLUSH PRIVILEGES;

SHOW GRANTS FOR 'read_only_user'@'localhost';
```

### Terminal Backup Command

```bash
mysqldump -u root -p store_db > store_db_backup.sql
```

## Explanation

1. `'read_only_user'@'localhost'` restricts login to localhost.
2. `GRANT SELECT ON store_db.*` provides read-only permission across all tables in `store_db`.
3. `mysqldump` exports DDL and DML statements to recreate the database.
