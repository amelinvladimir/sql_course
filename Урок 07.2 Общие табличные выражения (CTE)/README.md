# Общие табличные выражения (CTE)
```sql
with filtered_category as (
select
	fc.category_id,
	c."name" as category_name,
	count(*) as film_cnt
from
	film_category fc
join category c 
on
	fc.category_id = c.category_id
group by
	fc.category_id,
	c."name"
having
	count(*) > 70
)
select
	f.title,
	c.category_name,
	c.film_cnt as film_category_cnt
from
	film f
join film_category fc 
on
	f.film_id = fc.film_id
join filtered_category c
on
	c.category_id = fc.category_id;
```
```sql
select
	f.title,
	c.category_name,
	c.film_cnt as film_category_cnt
from
	film f
join film_category fc 
on
	f.film_id = fc.film_id
join (
	select
		fc.category_id,
		c."name" as category_name,
		count(*) as film_cnt
	from
		film_category fc
	join category c 
on
		fc.category_id = c.category_id
	group by
		fc.category_id,
		c."name"
	having
		count(*) > 70
) c
on
	c.category_id = fc.category_id;
```
```sql
with filtered_category as (
select
	fc.category_id,
	c."name" as category_name,
	count(*) as film_cnt
from
	film_category fc
join category c 
on
	fc.category_id = c.category_id
group by
	fc.category_id,
	c."name"
having
	count(*) > 70
),

film_amount as (
select
	i.film_id,
	sum(p.amount) as amount
from
	inventory i
join rental r 
on
	i.inventory_id = r.inventory_id
join payment p 
on
	p.rental_id = r.rental_id
group by
	i.film_id
),

total_amount as (
select
	sum(fa.amount) as total_amount
from
	film_amount fa
)

select
	f.title,
	c.category_name,
	c.film_cnt as film_category_cnt,
	coalesce(fa.amount, 0) as film_amount,
	ta.total_amount
from
	film f
join film_category fc 
on
	f.film_id = fc.film_id
join filtered_category c
on
	c.category_id = fc.category_id
left join film_amount fa
on
	fa.film_id = f.film_id
cross join total_amount ta;
```
```sql

with filtered_category as (
select
	fc.category_id,
	c."name" as category_name,
	count(*) as film_cnt
from
	film_category fc
join category c 
on
	fc.category_id = c.category_id
group by
	fc.category_id,
	c."name"
having
	count(*) > 70

),

film_amount as (
select
	i.film_id,
	sum(p.amount) as amount
from
	inventory i
join rental r 
on
	i.inventory_id = r.inventory_id
join payment p 
on
	p.rental_id = r.rental_id
group by
	i.film_id

),

total_amount as (
select
	sum(fa.amount) as total_amount
from
	film_amount fa
)
select
	*
from
	film_amount fa;
```
```sql
select
	*
from
	film_amount fa;
```
```sql
with filtered_category as materialized (
select
	fc.category_id,
	c."name" as category_name,
	count(*) as film_cnt
from
	film_category fc
join category c 
on
	fc.category_id = c.category_id
group by
	fc.category_id,
	c."name"
having
	count(*) > 70

),

film_amount as not materialized (
select
	i.film_id,
	sum(p.amount) as amount
from
	inventory i
join rental r 
on
	i.inventory_id = r.inventory_id
join payment p 
on
	p.rental_id = r.rental_id
group by
	i.film_id

),

total_amount as not materialized (
select
	sum(fa.amount) as total_amount
from
	film_amount fa

)

select
	f.title,
	c.category_name,
	c.film_cnt as film_category_cnt,
	coalesce(fa.amount, 0) as film_amount,
	ta.total_amount
from
	film f
join film_category fc 
on
	f.film_id = fc.film_id
join filtered_category c
on
	c.category_id = fc.category_id
left join film_amount fa
on
	fa.film_id = f.film_id
cross join total_amount ta;
```
