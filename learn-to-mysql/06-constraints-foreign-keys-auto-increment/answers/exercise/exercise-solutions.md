# Module 06 Exercise Solution

```sql
CREATE TABLE `projects` (
  `project_id` INT AUTO_INCREMENT PRIMARY KEY,
  `title` VARCHAR(100) NOT NULL
) ENGINE=InnoDB;

CREATE TABLE `tasks` (
  `task_id` INT AUTO_INCREMENT PRIMARY KEY,
  `description` TEXT NOT NULL,
  `project_id` INT NOT NULL,
  CONSTRAINT `fk_tasks_project`
    FOREIGN KEY (`project_id`) 
    REFERENCES `projects`(`project_id`) 
    ON DELETE CASCADE
) ENGINE=InnoDB;

INSERT INTO `projects` (`title`) VALUES ('Cloud Migration');
-- project_id = 1

INSERT INTO `tasks` (`description`, `project_id`) VALUES
  ('Audit servers', 1),
  ('Configure network', 1);

-- Deleting project 1 automatically cascades delete to tasks:
DELETE FROM `projects` WHERE `project_id` = 1;

SELECT COUNT(*) FROM `tasks`; -- Output: 0
```

## Explanation

1. `AUTO_INCREMENT` automatically assigns integer IDs starting at 1.
2. `ON DELETE CASCADE` causes deleting `project_id = 1` to immediately clean up dependent child rows in `tasks`.
