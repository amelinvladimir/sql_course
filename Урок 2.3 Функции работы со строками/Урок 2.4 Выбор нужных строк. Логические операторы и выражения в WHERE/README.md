# Выбор нужных строк. Логические операторы и выражения в WHERE.

```sql
select
	*
from
	film
where
	rental_rate = 4.99;
```

```sql
select
	*
from
	film
where
	rental_rate < 3;
```

```sql
select
	*
from
	film
where
	rental_rate >= 2.99;
```

```sql
select
	*
from
	rental
where
	rental_date between '2005-05-26' and '2005-05-28';
```

```sql
select
	*
from
	film
where
	title like '%Airport%';
```

```sql
select
	*
from
	film f
where
	description not like '%Epic%';
```

```sql
select
	*
from
	address a
where
	address2 is null;
```

```sql
select
	*
from
	address a
where
	address2 is not null;

```

```sql
select
	*
from
	film
where
	rental_duration != 7;
```

= > < >= <= like  not like  is null  is not null  <> != in between

```sql
select
	*
from
	film f
where
	not rental_duration = 7;
```

```sql
select
	*
from
	film f
where
	description not like '%Epic%';
```

```sql
select
	*
from
	film f
where
	not (description like '%Epic%');
```

```sql
select
	*
from
	film f
where
	rental_duration in (6, 7)
	and rental_rate > 1
	and title like 'P%';
```

```sql
select
	*
from
	film
where
	rental_duration = 1
	or rental_duration = 6
	or title like 'P%';
```

```sql
select
	*
from
	film f
where
	f.rental_duration in (6, 7)
	or f.rental_rate > 1
	and f.title like 'P%'
	or f.length between 70 and 120
	and f.rating = 'PG';
```

```sql
select
	*
from
	film f
where
	(
		rental_duration in (6, 7)
		or rental_rate > 1
	)
	and (
		title like 'P%'
		or length between 70 and 120
	)
	and rating = 'PG';
```
