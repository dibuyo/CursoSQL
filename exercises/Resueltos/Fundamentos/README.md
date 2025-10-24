# Resueltos

A continuación se dejan los resueltos de los ejercicios de la sección 1.Fundamentos:

1.
```sql
SELECT * FROM [movie];
```

2.
```sql
SELECT * FROM [movie] WHERE title LIKE '%Back to the Future%';
```

3.
```sql
SELECT COUNT(*) AS qty FROM [movie] WHERE title LIKE '%Terminator%';
```

4.
```sql
SELECT COUNT(*) FROM [movie] WHERE runtime > 120;
```

5.
```sql
SELECT TOP 1 * FROM [movie] ORDER BY runtime DESC;

SELECT  * FROM [movie] ORDER BY runtime DESC LIMIT 1;
```

6.
```sql
SELECT YEAR(release_date) AS ANIO, COUNT(*) AS qty FROM [movie] GROUP BY YEAR(release_date) ORDER BY 1;
```

7.
```sql
SELECT 
    movie_id,
    title,
    SUM(CAST(hours_viewed AS BIGINT)) AS total_hours_viewed
FROM [view_summary]
INNER JOIN [movie] 
    ON view_summary.movie_id = movie.id
GROUP BY movie_id, title
ORDER BY total_hours_viewed DESC;
```