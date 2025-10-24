# Resueltos

A continuación se dejan los resueltos de los ejercicios de la sección 2.Avanzado:

1.
```sql
SELECT 
    a.au_lname AS Apellido,
    a.au_fname AS Nombre,
    t.title AS Titulo,
    p.pub_name AS Editorial
FROM authors AS a
INNER JOIN titleauthor AS ta 
    ON a.au_id = ta.au_id
INNER JOIN titles AS t 
    ON ta.title_id = t.title_id
INNER JOIN publishers AS p 
    ON t.pub_id = p.pub_id
ORDER BY a.au_lname, a.au_fname;
```

2.
```sql
SELECT 
    p.pub_name AS Editorial,
    COUNT(t.title_id) AS Cantidad_Libros,
    AVG(t.price) AS Promedio_Precio
FROM publishers AS p
INNER JOIN titles AS t 
    ON p.pub_id = t.pub_id
GROUP BY p.pub_name
ORDER BY Promedio_Precio DESC;
```