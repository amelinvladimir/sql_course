# Представления
```sql
create view film_amount as 
select
	f.film_id,
	sum(p.amount) as amount
from
	film f
left join inventory i 
on
	i.film_id = f.film_id
left join rental r 
on
	r.inventory_id = i.inventory_id
left join payment p 
on
	p.rental_id = r.rental_id
group by
	f.film_id;
```
```sql
explain
select
	*
from
	film_amount;
```
```sql
explain
select
	f.film_id,
	sum(p.amount) as amount
from
	film f
left join inventory i 
on
	i.film_id = f.film_id
left join rental r 
on
	r.inventory_id = i.inventory_id
left join payment p 
on
	p.rental_id = r.rental_id
group by
	f.film_id;
```
```sql
create materialized view film_amount_mat as 
select
	f.film_id,
	sum(p.amount) as amount
from
	film f
left join inventory i 
on
	i.film_id = f.film_id
left join rental r 
on
	r.inventory_id = i.inventory_id
left join payment p 
on
	p.rental_id = r.rental_id
group by
	f.film_id;
```
```sql
explain
select
	*
from
	film_amount_mat;
```
```sql
explain
select
	f1.*
from
	film_amount f1
join film_amount f2
on
	f1.film_id = f2.film_id;
```
```sql
explain
select
	f1.*
from
	film_amount_mat f1
join film_amount_mat f2
on
	f1.film_id = f2.film_id;
```
```sql
refresh materialized view film_amount_mat;
```
