# Подзапросы

```sql
select
	*
from
	address a;

```
```sql
select
	*
from
	customer c;
```
```sql
select
	*
from
	address a
where
	not exists(
	select
		1
	from
		customer c
	where
		c.address_id = a.address_id 

);
```
```sql
select
	*
from
	customer c
where
	c.address_id = 5;
```
```sql
select
	*
from
	film f
where
	f.rental_duration in (3, 4);
```
```sql
select
	fc.category_id
from
	film_category fc
group by
	fc.category_id
having
	count(*) > 70;
```
```sql
select
	f.title,
	c."name" as category_name
from
	film f
join film_category fc 
on
	fc.film_id = f.film_id
join category c 
on
	c.category_id = fc.category_id
where
	c.category_id in (
	select
		fc.category_id
	from
		film_category fc
	group by
		fc.category_id
	having
		count(*) > 70

);
```
```sql
select
	1 in (1, 2);
--true
```
```sql
select
	1 in (2, 3);
--false
```
```sql
select
	1 in (1, 2, null);
--true
```
```sql
select
	1 in (2, 3, null);
--null
```
```sql
select
	null in (1, 2, null);
--null
```
```sql
select
	distinct p.amount
from
	payment p
order by
	p.amount ;
```
```sql
select
	*
from
	payment p
where
	p.amount > any(
	select
		p2.amount
	from
		payment p2 

)
order by
	p.amount;
```
```sql
select
	*
from
	payment p
where
	p.amount >= all(
	select
		p2.amount
	from
		payment p2 

)
order by
	p.amount;
```
```sql
select
	f.title,
	f.rating,
	(
	select
		count(*)
	from
		film f2
	where
		f2.rating = f.rating 

) as film_rating_cnt,
	(
	select
		count(*)
	from
		film f2

) as film_cnt,
	(
	select
		c."name"
	from
		film_category fc
	join category c 

on
		c.category_id = fc.category_id
	where
		fc.film_id = f.film_id 

) as category_name
from
	film f;
```
```sql
select
	f.title
from
	film f
where
	10 < (
	select
		count(*)
	from
		film_actor fa
	where
		fa.film_id = f.film_id 

);
```
```sql
select
	f.rating,
	count(*) as cnt
from
	film f
group by
	f.rating;
```
```sql
select
	f.title,
	f.rating,
	fr.cnt as rating_film_cnt
from
	film f
join (
	select
		f.rating,
		count(*) as cnt
	from
		film f
	group by
		f.rating 

) fr

on
	f.rating = fr.rating;
```
