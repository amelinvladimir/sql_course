# Условия в выражениях с помощью Case
```sql
select
	a.first_name || ' ' || a.last_name as actor_name,
	length(a.first_name || ' ' || a.last_name),
	case
		when length(a.first_name || ' ' || a.last_name) > 15

then substring(a.first_name, 1, 7) || ' ' || substring(a.last_name, 1, 7)
		else a.first_name || ' ' || a.last_name
	end as short_name
from
	actor a;

```
```sql
select
	case
		when length(a.first_name || ' ' || a.last_name) > 15
then substring(a.first_name, 1, 7) || ' ' || substring(a.last_name, 1, 7)
		else a.first_name || ' ' || a.last_name
	end as short_name
from
	actor a
where
	substring(
case
when length(a.first_name || ' ' || a.last_name) > 15
then substring(a.first_name, 1, 7) || ' ' || substring(a.last_name, 1, 7)
else a.first_name || ' ' || a.last_name
end,
1, 
2
) = 'ca'
order by
	case
		when length(a.first_name || ' ' || a.last_name) > 15
then substring(a.first_name, 1, 7) || ' ' || substring(a.last_name, 1, 7)
		else a.first_name || ' ' || a.last_name
	end;

```
```sql
select
	f.title,
	l."name",
	case
		when l."name" = 'english' then 'английский'
		when l."name" = 'italian' then 'итальянский'
		when l."name" = 'japanese' then 'японский'
		when l."name" = 'mandarin' then 'китайский'
		when l."name" = 'french' then 'французский'
		when l."name" = 'german' then 'немецкий'
		else 'неизвестный язык'
	end,
	case
		l."name"
when 'english' then 'английский'
		when 'italian' then 'итальянский'
		when 'japanese' then 'японский'
		when 'mandarin' then 'китайский'
		when 'french' then 'французский'
		when 'german' then 'немецкий'
		else 'неизвестный язык'
	end
from
	film f
join "language" l 
on
	f.language_id = l.language_id;

```
```sql
select
	f.title,
	l."name",
	case
		when l."name" = 'english' then 'английский'
		when l."name" = 'italian' then 'итальянский'
		when l."name" = 'japanese' then 'японский'
		when l."name" = 'mandarin' then 'китайский'
		when l."name" = 'french' then 'французский'
		when l."name" = 'german' then 'немецкий'
		else 'неизвестный язык'
	end,
	f.rating,
	f.language_id,
	l.language_id
from
	film f
join "language" l 
on
	case
		when f.rating = 'g' then 2
		else f.language_id
	end = l.language_id;
```
```sql
select
	f.title,
	sum(p.amount) as total_amount,
	case
		when sum(p.amount) >= 150 then 'top amount'
		when sum(p.amount) >= 100 then 'middle amount'
		else 'low amount'
	end as amount_rating
from
	film f
join inventory i
		using(film_id)
join rental r
		using(inventory_id)
join payment p
		using(rental_id)
group by
	f.title;
```
```sql
select
	case
		when div(f.rental_rate, 1) = 0 then 0
		else 1 / div(f.rental_rate, 1)
	end
from
film f;
```
