# Module 27: Walk Hierarchies with Recursive CTEs

## What you will learn

You will follow parent-child relationships repeatedly while controlling termination and cycles.

## A recursive CTE has two parts

```sql
WITH RECURSIVE organization AS (
  SELECT employee_id, name, manager_id, 0 AS depth
  FROM employees
  WHERE manager_id IS NULL

  UNION ALL

  SELECT e.employee_id, e.name, e.manager_id, o.depth + 1
  FROM employees AS e
  JOIN organization AS o
    ON e.manager_id = o.employee_id
)
SELECT employee_id, name, depth
FROM organization
ORDER BY depth, employee_id;
```

The first query is the anchor. It finds starting rows. The second is the recursive member. It joins new rows to rows already found. Recursion stops when an iteration produces no new rows.

## The relationship must move toward termination

Here, every step finds direct reports of previously found employees. A wrong join can repeat forever until SQLite's limits stop it or can create an enormous result.

Test with a small depth guard during development:

```sql
WHERE o.depth < 20
```

The guard prevents runaway work but does not correct cyclic data.

## Protect against cycles

A hierarchy can accidentally contain A reporting to B and B reporting to A. Prevent cycles during writes where possible. For defensive reads, maintain a visited path with unambiguous delimiters and refuse an identifier already present.

```sql
WITH RECURSIVE chain(employee_id, name, manager_id, path) AS (
  SELECT employee_id, name, manager_id, ',' || employee_id || ','
  FROM employees
  WHERE employee_id = 1

  UNION ALL

  SELECT e.employee_id, e.name, e.manager_id,
         chain.path || e.employee_id || ','
  FROM employees AS e
  JOIN chain ON e.manager_id = chain.employee_id
  WHERE instr(chain.path, ',' || e.employee_id || ',') = 0
)
SELECT * FROM chain;
```

This SQLite text-path technique is educational, not a universal high-scale graph solution.

## UNION compared with UNION ALL

`UNION` removes duplicate complete rows and can sometimes stop repetition, but added depth or path columns make rows different. It also adds duplicate-removal work. Design explicit termination rather than depending on it accidentally.

## Hierarchies are not every graph problem

Recursive SQL can traverse graphs, but complex path finding, very deep graphs, and frequent relationship changes may need specialized modeling and careful indexes. Measure the real workload.

## Common mistakes

### Reversing the parent-child join

Say which direction each step travels and test one level first.

### Forgetting an anchor restriction

Starting from every row can repeat overlapping trees.

### Assuming valid foreign keys prevent cycles

They ensure referenced rows exist, not that the graph is acyclic.

## Check your understanding

You are ready when you can identify the anchor, recursive step, termination condition, and cycle strategy.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
