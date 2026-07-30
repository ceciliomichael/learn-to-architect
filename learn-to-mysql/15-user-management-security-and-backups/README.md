# Module 15: User Privilege Management, Security, and Backups

## What You Will Learn

In this module, you will learn how to manage multi-user security in MySQL, create user accounts with host restrictions (`CREATE USER`), grant and revoke granular database privileges (`GRANT`, `REVOKE`), flush privileges (`FLUSH PRIVILEGES;`), and perform command-line database backup and restore operations using `mysqldump`.

---

## User Management & Privilege Enforcement

In MySQL, a user identity consists of both a **username** and a **host specification** (`'username'@'host'`).

```sql
-- Create a user allowed to connect only from localhost
CREATE USER 'app_user'@'localhost' IDENTIFIED BY 'StrongPassword123!';

-- Create a user allowed to connect from any remote host ('%')
CREATE USER 'reporter'@'%' IDENTIFIED BY 'ReporterPass456!';
```

---

## Granting and Revoking Privileges

Apply the **Principle of Least Privilege**:

```sql
-- Grant read/write access to specific database
GRANT SELECT, INSERT, UPDATE, DELETE ON `store_db`.* TO 'app_user'@'localhost';

-- Grant read-only access
GRANT SELECT ON `store_db`.* TO 'reporter'@'%';

-- Reload privilege tables into memory
FLUSH PRIVILEGES;

-- Inspect active grants
SHOW GRANTS FOR 'app_user'@'localhost';
```

To revoke permissions:
```sql
REVOKE DELETE ON `store_db`.* FROM 'app_user'@'localhost';
```

---

## Database Backup and Restore (`mysqldump`)

`mysqldump` is a command-line utility for exporting database schemas and data into executable `.sql` text scripts:

### Backup Command (Run in terminal, not MySQL prompt)
```bash
mysqldump -u root -p store_db > store_db_backup.sql
```

### Restore Command
```bash
mysql -u root -p store_db < store_db_backup.sql
```

---

## Check Your Understanding

1. Why does MySQL identify users as `'user'@'host'` rather than just `'user'`?
2. What command exports a complete SQL dump script of a database from the command line?
