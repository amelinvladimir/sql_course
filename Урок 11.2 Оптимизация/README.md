# Оптимизация
```sql
select
	*
from
	film;
```
```sql
explain analyze
select
	*
from
	film;
```
```sql
explain analyze
select
	*
from
	film
where
	length > 150;
```
```sql
explain analyze
select
	*
from
	film
where
	length > 180;
```
```sql
create index film_length_idx on
film(length);
```
```sql
drop index film_length_idx;
```
- min index scan
- middle bitmap index scan
- max seq scan

```sql
explain analyze
select
	f.title,
	p.amount
from
	film f
join inventory i
		using(film_id)
join rental r
		using(inventory_id)
join payment p
		using(rental_id);
```
