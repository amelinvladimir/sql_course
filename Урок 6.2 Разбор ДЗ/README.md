# Разбор домашнего задания 6.2
Все фильмы (film) нужно сгруппировать по рейтингу (film.rating). И для каждой группы вывести 3 поля:
- Название рейтинга (film.rating)
- Сколько всего фильмов с данным рейтингом
- Сколько фильмов с данным рейтингом и продолжительностью сдачи в аренду 5 или больше (film.rating_duration >= 5)
```sql
select
	f.rating,
	count(*) as film_total_cnt,
	count(*) filter(
	where f.rental_duration >= 5) as film_five_more_rent_dur_cnt
from
	film f
group by
	f.rating;
```
Задания для повторения и закрепления пройденных тем

Запросите топ-3 стран с наибольшим количеством клиентов проката. Выведите 2 поля: страна(country.country), количество клиентов. Используйте join, count, limit.
```sql
select
	c3.country ,
	count (c.customer_id) customers_number
from
	customer c
join

address a
		using (address_id)
join city c2
		using(city_id)
join country c3
		using (country_id)
group by
	c3.country
order by
	2 desc
limit 3;

```

