# frozen
Frozen DuckLake Demo

Run this command to see the serverless Frozen Ducklake demo hosted on GitHub:
```
duckdb ducklake:https://raw.githubusercontent.com/marhar/frozen/main/space.ducklake
```

Some queries:
```sql
SHOW TABLES;

SELECT
    m.name as mission, 
    count(DISTINCT a.nationality) AS nationalities,
    string_agg(DISTINCT a.nationality, ', ') AS countries_represented
FROM missions m
JOIN mission_crew mc ON m.mission_id = mc.mission_id
JOIN astronauts a ON mc.astronaut_id = a.astronaut_id
WHERE mc.primary_crew = true
GROUP BY m.mission_id, m.name
HAVING count(DISTINCT a.nationality) > 1
ORDER BY nationalities DESC
LIMIT 4;
```
