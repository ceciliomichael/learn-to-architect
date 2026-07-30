# Module 04 Exercise Solution

```sql
SELECT player, score 
FROM scores 
ORDER BY score DESC, player ASC 
LIMIT 2 OFFSET 1;
```

### Expected Output

```text
┌────────┬───────┐
│ player │ score │
├────────┼───────┤
│ Bob    │ 520   │
│ Eve    │ 520   │
└────────┴───────┘
```

## Explanation

1. `ORDER BY score DESC, player ASC` ranks scores highest first, using alphabetical player name as a tiebreaker.
2. `LIMIT 2 OFFSET 1` skips the 1st row (Diana with 610) and returns the next 2 rows (Bob and Eve with 520).
