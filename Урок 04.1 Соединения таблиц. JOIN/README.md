# Соединения таблиц. JOIN

```sql
SELECT
	*
FROM
	film;
```

```sql
SELECT
	*
FROM
	"language" l;
```

```sql
SELECT
	f.title,
	l."name" AS language_name
FROM
	film f
INNER JOIN "language" l

ON
	f.language_id = l.language_id
WHERE
	f.title LIKE 'C%';
```

```sql
SELECT DISTINCT
        a.first_name || ' ' || a.last_name AS actor_name
FROM
	film_actor fa
INNER JOIN actor a 
ON
	fa.actor_id = a.actor_id
INNER JOIN film f 
ON
	fa.film_id = f.film_id
INNER JOIN inventory i 
ON
	i.film_id = f.film_id ;
```

```sql
SELECT
	*
FROM
	actor;
```

```sql
SELECT
	*
FROM
	inventory i;
```

```sql
SELECT DISTINCT
        a.first_name || ' ' || a.last_name AS actor_name
FROM
	film_actor fa
INNER JOIN actor a
		USING (actor_id)
INNER JOIN film f
		USING (film_id)
INNER JOIN inventory i
		USING (film_id);

```

```sql
SELECT
	f.title
FROM
	film f
LEFT JOIN inventory i
		USING (film_id)
WHERE
	i.inventory_id IS NULL;
```

```sql
SELECT
	f.title
FROM
	inventory i
RIGHT JOIN film f
		USING (film_id)
WHERE
	i.inventory_id IS NULL;
```

```sql
SELECT
	f.title
FROM
	inventory i
FULL JOIN film f
		USING (film_id)
WHERE
	i.inventory_id IS NULL;
```

```sql
SELECT
	f.title,
	a.first_name || ' ' || a.last_name AS actor_name
FROM
	film f
CROSS JOIN actor a;

```
```sql
SELECT
	f.title,
	a.first_name || ' ' || a.last_name AS actor_name
FROM
	film f
INNER JOIN actor a
ON
	TRUE;
```
```sql
SELECT 
        f.title,
        a.first_name || ' ' || a.last_name AS actor_name
FROM 
        film f,actor a;
```
```sql
SELECT
	f.title,
	a.first_name || ' ' || a.last_name AS actor_name,
	fa.actor_id IS NOT NULL
FROM
	film f
CROSS JOIN actor a
LEFT JOIN film_actor fa 
ON
	fa.film_id = f.film_id
	AND fa.actor_id = a.actor_id ;
```


