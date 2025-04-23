# Порядок выполнения частей запроса
```sql
select
	f.title,
	f.rating,
	count(*) over(partition by f.rating) as film_rating_cnt
from
	film f
limit 10;

        -- 1 with
with film_amount as (
select
	i.film_id,
	sum(p.amount) as total_amount
from
	inventory i
join rental r
		using (inventory_id)
join payment p
		using (rental_id)
group by
	i.film_id
)
        -- 6 select
        -- 7 distinct
select
	distinct
substring(f.title, 1, 3) as short_title,
	f.rental_duration,
	count(*) over(partition by f.rental_duration) as rent_dur_film_cnt,
	sum(fa.total_amount) as total_amount
	-- 2 from
from
	film f
join film_amount fa
		using (film_id)
	-- 3 where
where
	f.rating = 'g'
	-- 4 group by
group by
	substring(f.title, 1, 3),
	f.rental_duration
	-- 5 having
having
	count(*) = 1
	-- 8 order by
order by
	total_amount
	-- 9 limit offset
limit 10
offset 5;

```
