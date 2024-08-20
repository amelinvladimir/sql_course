# Получение части строк в результате с помощью Limit и Offset
```sql
select
	f.title
from
	film f
order by
	f.title
limit 50;
```
```sql
select
	f.title
from
	film f
order by
	f.title
limit 50
offset 50;
```
```sql
select
	f.title
from
	film f
order by
	f.title
limit 50
offset 100;
```
```sql
select
	f.title
from
	film f
order by
	f.title 
offset 500;
```
```sql
select
	f.title
from
	film f
order by
	f.title
limit all
offset 500;
```
```sql
select
	f.title
from
	film f
order by
	f.title
limit null
offset 500;
```
```sql
select
	f.title,
	sum(p.amount) as total_amount
from
	film f
join inventory i
		using (film_id)
join rental r
		using (inventory_id)
join payment p
		using (rental_id)
group by
	f.title
order by
	total_amount desc
limit 25
offset 25;
```

