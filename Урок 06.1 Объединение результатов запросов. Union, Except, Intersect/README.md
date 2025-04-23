# Объединение результатов запросов. Union, Except, Intersect

```sql
select
	f.title,
	'amount' as src
from
	film f
join inventory i
		using(film_id)
join rental r
		using(inventory_id)
join payment p
		using (rental_id)
group by
	f.title
having
	sum(p.amount) > 150
union all
select
	f.title,
	'rental rate' as src
from
	film f
where
	f.rental_rate > 4;

```
```sql
select
	f.title,
	'amount' as src
from
	film f
join inventory i
		using(film_id)
join rental r
		using(inventory_id)
join payment p
		using (rental_id)
group by
	f.title
having
	sum(p.amount) > 150
union
select
	f.title as some_alias,
	'rental rate' as some_alias2
from
	film f
where
	f.rental_rate > 4;
```
```sql
select
	f.title,
	f.rental_rate,
	f.rental_duration,
	f.rating,
	'amount' as src
from
	film f
join inventory i
		using(film_id)
join rental r
		using(inventory_id)
join payment p
		using (rental_id)
group by
	f.title,
	f.rental_rate,
	f.rental_duration,
	f.rating
having
	sum(p.amount) > 150
union all
select
	f.title as some_alias,
	f.rental_rate,
	f.rental_duration,
	f.rating,
	'rental rate' as some_alias2
from
	film f
where
	f.rental_rate > 4
union all
select
	f.title as some_alias,
	f.rental_rate,
	f.rental_duration,
	f.rating,
	'rental duration' as src
from
	film f
where
	f.rental_duration = 3;
```
```sql
select
	f.title,
	f.rental_rate,
	f.rental_duration,
	f.rating,
	'amount' as src
from
	film f
join inventory i
		using(film_id)
join rental r
		using(inventory_id)
join payment p
		using (rental_id)
group by
	f.title,
	f.rental_rate,
	f.rental_duration,
	f.rating
having
	sum(p.amount) > 150
union all
select
	f.title as some_alias,
	f.rental_rate,
	f.rental_duration,
	f.rating,
	'rental rate' as some_alias2
from
	film f
where
	f.rental_rate > 4
	or f.rental_duration = 3;
```
```sql
select
	f.title,
	f.rental_rate,
	f.rental_duration,
	f.rating
from
	film f
join inventory i
		using(film_id)
join rental r
		using(inventory_id)
join payment p
		using (rental_id)
group by
	f.title,
	f.rental_rate,
	f.rental_duration,
	f.rating
having
	sum(p.amount) > 150
except
select
	f.title as some_alias,
	f.rental_rate,
	f.rental_duration,
	f.rating
from
	film f
where
	f.rating = 'g';
```
```sql
select
	f.title,
	f.rental_rate,
	f.rental_duration,
	f.rating
from
	film f
join inventory i
		using(film_id)
join rental r
		using(inventory_id)
join payment p
		using (rental_id)
group by
	f.title,
	f.rental_rate,
	f.rental_duration,
	f.rating
having
	sum(p.amount) > 150
intersect
select
	f.title as some_alias,
	f.rental_rate,
	f.rental_duration,
	f.rating
from
	film f
where
	f.rating = 'g';
```
