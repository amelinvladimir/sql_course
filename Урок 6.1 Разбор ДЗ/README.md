# Разбор домашнего задания 6.1
1.Получить список названий всех фильмов (film.title), рекомендованных для просмотра самыми маленькими зрителями.
Для этого нужно объединить результаты выполнения двух запросов:1) получить все фильмы (film) с рейтингом G (film.rating = 'G') 2) получить все фильмы (film), в которых снимался актер с фамилией Grant (actor.last_name = 'Grant'), поскольку этот актер по умолчанию снимается только в фильмах для самых маленьких вне зависимости от проставленного рейтинга.
Если какой-то фильм попадет в оба запроса, то его нужно вывести дважды. Решить задачу с использованием union/union all/except/intersect
```sql
select
	f.title
from
	film f
where
	f.rating = 'g'
union all
select
	f.title
from
	film f
join film_actor fa
		using(film_id)
join actor a
		using(actor_id)
where
	a.last_name = 'grant';

```
2.Получить список названий всех фильмов (film.title) с рейтингом G (film.rating = 'G'), в которых снимался актер с фамилией Grant (actor.last_name = 'Grant').
Решить задачу с использованием union/union all/except/intersect
```sql

select
	f.title
from
	film f
where
	f.rating = 'g'
intersect
select
	f.title
from
	film f
join film_actor fa
		using(film_id)
join actor a
		using(actor_id)
where
	a.last_name = 'grant';
```
3.Получить список названий всех фильмов (film.title) с рейтингом НЕ G (film.rating <> 'G'), в которых снимался актер с фамилией Grant (actor.last_name = 'Grant'). 
Решить задачу с использованием union/union all/except/intersect
```sql
select
	f.title
from
	film f
join film_actor fa
		using(film_id)
join actor a
		using(actor_id)
where
	a.last_name = 'grant'
except
select
	f.title
from
	film f
where
	f.rating = 'g';
```
Задание для повторения и закрепления пройденных тем

Запросите список клиентов проката(customer), которые проживают в Калифорнии (address.district)
Выведите 3 поля: фамилия клиента(customer.last_name), адрес(address.address), район(address.district) Используйте join, where.
```sql
select
	c.last_name,
	a.address,
	a.district
from
	customer c
join address a
on
	c.address_id = a.address_id
WHERE district ='California'
```
