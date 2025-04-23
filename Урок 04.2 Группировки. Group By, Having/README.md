# Группировки. Group By, Having
```sql
select
	rating,
	count(*) films_count,
	sum(length) as total_length,
	max(length) as max_length,
	min(length) as min_length,
	avg(length) as avg_length,
	bool_and(length < 185) ,
	bool_or(length >= 185),
	string_agg(title, '; ')
from
	film f
group by
	rating;

```
```sql
select distinct 
       rating
from 
       film;

```
```sql
select 
       count(*),
       sum(length)
from 
	film f
```
```sql
select 
	rating,
	rental_rate,
	substring(title, 1, 1),
	count(*)
from 
	film f
group by
	rating,
	rental_rate,
	substring(title, 1, 1)
order by 
	rating,
	rental_rate;

```
```sql
select 
	title,
	count(*)
from 
	inventory i
join film f
		using (film_id)
group by
	title;
```
```sql
select 
	f.title,
	f.film_id,
	i.film_id
from 
	film f
left join inventory i 
		on
	f.film_id = i.film_id
order by 
	i.film_id;
```
```sql
select 
	f.title,
	count(i.film_id) film_count
from 
	film f
left join inventory i 
		on
	f.film_id = i.film_id
group by 
	f.title
order by
	film_count;
```

```sql
select 
	f.title,
	count(fc.film_id) as category_count
from 
	film f
left join film_category fc 
		on
	f.film_id = fc.film_id
group by 
	f.title
order by 
	category_count;
```

```sql
select 
	a.first_name || ' ' || a.last_name as actor_name,
	fa.film_id,
	fc.category_id
from 
	actor a
join film_actor fa
		using(actor_id)
join film_category fc
		using(film_id);
```
```sql
select 
	a.first_name || ' ' || a.last_name as actor_name,
	count(*) as film_count,
	count(distinct fc.category_id) as category_count
from 
	actor a
join film_actor fa
		using(actor_id)
join film_category fc
		using(film_id)
group by
	a.first_name || ' ' || a.last_name;
```
```sql
select 
	f.title,
	count(*) as payment_count
from 
	film f
join inventory i on
	f.film_id = i.film_id
join rental r on
	r.inventory_id = i.inventory_id
join payment p on
	p.rental_id = r.rental_id
where 
	f.rental_rate > 2
group by 
	f.title
having 
	count(*) > 10
order by 
	payment_count;
```
