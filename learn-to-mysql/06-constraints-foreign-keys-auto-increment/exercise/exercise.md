# Module 06 Exercise

1. Create a parent table `projects` (`project_id` INT AUTO_INCREMENT PRIMARY KEY, `title` VARCHAR(100)).
2. Create a child table `tasks` (`task_id` INT AUTO_INCREMENT PRIMARY KEY, `description` TEXT, `project_id` INT, FOREIGN KEY referencing `projects` with `ON DELETE CASCADE`).
3. Insert 1 project, 2 tasks, and delete the project to observe automatic cascade deletion of tasks.
