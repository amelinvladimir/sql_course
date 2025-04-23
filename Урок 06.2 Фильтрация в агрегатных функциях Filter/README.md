# Фильтрация в агрегатных функциях Filter

```sql
select
	count(*),
	count(*) filter(
	where length > 100),
	count(*) filter(
	where length > 120),
	count(*) filter(
	where length > 140)
from
	film;
```
```sql
select
	f.rating,
	count(*),
	count(*) filter(
	where length > 100),
	count(*) filter(
	where length > 120),
	count(*) filter(
	where length > 140)
from
	film f
group by
	f.rating;
```
```sql
select
	*
from
	film f
order by
	rating,
	length desc;
```
```sql
select
	count(*)
from
	film
where
	length > 100;
```

