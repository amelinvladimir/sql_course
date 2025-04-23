# Оконные функции
```sql
select
	f.title,
	f.rating,
	f.length,
	min(f.length) over(partition by f.rating) as min_rating_length,
	max(f.length) over(partition by f.rating) as max_rating_length,
	sum(f.length) over(partition by f.rating) as sum_rating_length,
	avg(f.length) over(partition by f.rating) as avg_rating_length,
	count(f.length) over(partition by f.rating) as count_rating_length,
	min(f.length) over() as min_rating_length
from
	film f
order by
	f.rating,
	f.length;
```
```sql
select
	f.title,
	f.rating,
	f.length,
	min(f.length) over w as min_rating_length,
	max(f.length) over w as max_rating_length,
	sum(f.length) over w as sum_rating_length,
	avg(f.length) over w as avg_rating_length,
	count(f.length) over w as count_rating_length
from
	film f 

window w as (partition by f.rating)
order by
	f.rating,
	f.length;
```
```sql
select
	f.title,
	f.rating,
	f.length,
	row_number() over(partition by f.rating) as rn,
	row_number() over(partition by f.rating
order by
	f.length) as rn,
	rank() over(partition by f.rating
order by
	f.length) as rk,
	dense_rank() over(partition by f.rating
order by
	f.length) as drk
from
	film f;
```
```sql
select
	f.title,
	f.rating,
	f.length,
	lag(f.length, 1) over(partition by f.rating
order by
	f.length) as prev_length,
	lead(f.length, 1) over(partition by f.rating
order by
	f.length) as next_length,
	f.length - lag(f.length, 1) over(partition by f.rating
order by
	f.length) as diff_length
from
	film f;
```
```sql
select
	c."name",
	c.category_id,
	ntile(3) over(
	order by category_id) as group_id
from
	category c;
```
```sql
select
	r.rental_date::date,
	count(*) as cnt,
	lag(count(*), 1) over(
	order by r.rental_date::date) as prev_cnt,
	count(*) - lag(count(*), 1) over(
	order by r.rental_date::date) as diff_cnt
from
	rental r
group by
	r.rental_date::date
order by
	r.rental_date::date;
```
```sql

with rent_day as (
	select
		r.rental_date::date as rent_day,
		count(*) as cnt
	from
		rental r
	group by
		r.rental_date::date

)

select
	r.rent_day,
	r.cnt,
	sum(r.cnt) over(
	order by r.rent_day rows between 2 preceding and current row) as three_days_cnt,
	sum(r.cnt) over(
	order by r.rent_day rows between current row and current row) as current_cnt,
	sum(r.cnt) over(
	order by r.rent_day rows between 3 preceding and 3 following) as week_cnt,
	sum(r.cnt) over(
	order by r.rent_day rows between unbounded preceding and current row) as week_cnt,
	sum(r.cnt) over(
	order by r.rent_day rows between unbounded preceding and unbounded following) as total_cnt
from
	rent_day r;
```
```sql
select
	f.title,
	f.rating,
	f.length,
	sum(f.length) over(partition by f.rating
order by
	f.length rows between unbounded preceding and current row) as cum_length_row,
	sum(f.length) over(partition by f.rating
order by
	f.length range between unbounded preceding and current row) as cum_length_range,
	sum(f.length) over(partition by f.rating
order by
	f.length),
	sum(f.length) over(partition by f.rating),
	sum(f.length) over(partition by f.rating
order by
	f.length,
	f.film_id),
	sum(f.length) over(partition by f.rating
order by
	f.length range between current row and unbounded following)
from
	film f;
```
```sql
select
	f.title,
	f.rating,
	f.length,
	first_value(f.length) over(partition by f.rating
order by
	f.length) as frst_length,
	last_value(f.length) over(partition by f.rating
order by
	f.length) as lst_length,
	last_value(f.length) over(partition by f.rating
order by
	f.length range between unbounded preceding and current row) as lst_length,
	last_value(f.length) over(partition by f.rating
order by
	f.length range between unbounded preceding and unbounded following) as lst_length
from
film f ;
```
