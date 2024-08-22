# Разбор домашнего задания 5.1
1.Вывести список всех фильмов (film). По каждому фильму отобразить 3 поля: 1. название фильма (film.title) 2. рейтинг фильма (film.rating) 3. расшифровку рейтинга фильма.  Ниже указаны пары: рейтинг - расшифровка рейтинга:
G - Нет возрастных ограничений,
PG - Рекомендуется присутствие родителей,
PG-13 - Детям до 13 лет просмотр не желателен,
R - Лицам до 17 лет обязательно присутствие взрослого,
NC-17 - Лицам до 18 лет просмотр запрещен 
```sql
select
	f.title,
	f.rating,
	case
		when f.rating = 'g' then 'нет возрастных ограничений'
		when f.rating = 'pg' then 'рекомендуется присутствие родителей'
		when f.rating = 'pg-13' then 'детям до 13 лет просмотр не желателен'
		when f.rating = 'r' then 'лицам до 17 лет обязательно присутствие взрослого'
		when f.rating = 'nc-17' then 'лицам до 18 лет просмотр запрещен'
		else 'неизвестный рейтинг'
	end as rating_full
from
	film f;
```
```sql
select
	f.title,
	f.rating,
	case
		f.rating
when 'g' then 'нет возрастных ограничений'
		when 'pg' then 'рекомендуется присутствие родителей'
		when 'pg-13' then 'детям до 13 лет просмотр не желателен'
		when 'r' then 'лицам до 17 лет обязательно присутствие взрослого'
		when 'nc-17' then 'лицам до 18 лет просмотр запрещен'
		else 'неизвестный рейтинг'
	end as rating_full
from
	film f;
```
2.Вывести 3 колонки: 1. название фильма (film.title) 2. рейтинг фильма (film.rating) 3. продолжительность фильма. Отобразить только фильмы продолжительностью более 120 (film.length > 120). 
Для фильмов с рейтингом G при проверке брать удвоенную продолжительность (film.length * 2 > 120). При написании условия отбора фильмов использовать case. 
```sql
select
	f.title,
	f.rating,
	f.length
from
	film f
where
	case
		when f.rating = 'g' then f.length * 2
		else f.length
	end > 120;

```
```sql
select
	f.title,
	f.rating,
	f.length
from
	film f
where
	f.length > case
		when f.rating = 'g' then 60
		else 120
	end;
```
3.Вывести список всех фильмов (film). По каждому фильму нужно отобразить 2 колонки: 1. название фильма (film.title) 2. название категории фильма (category.name). Если фильм относится к категории с category_id = 5, то вместо категории с идентификатором 5 нужно отобразить категорию с category_id = 1.
Связь между таблицей фильмов (film) и таблицей категорий (category) осуществляется посредствам промежуточной таблицы film_category.
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
	case
		when fc.category_id = 5 then 1
		else fc.category_id
	end = c.category_id;
```
