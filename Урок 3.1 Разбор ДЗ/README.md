# Разбор домашнего задания 3.1
1.Из таблицы фильмов (film) запросить 2 поля: title и length. 
Полю length дать имя - "len".
Отсортировать полученный результат по продолжительности фильма (по полю length).
Написать запрос в 3 вариантах с сортировкой:
1. по имени поля в таблице (length)
2. по номеру столбца в результирующем наборе
3. по имени столбца в результирующем наборе

```sql
select
	title,
	length as len
from
	film
order by
	length;
```

```sql
select
	title,
	length as len
from
	film
order by
	2;
```

```sql
select
	title,
	length as len
from
	film
order by
	len;
```

2.Из таблицы фильмов (film) запросить 3 поля: length, rental_duration, title. Отсортировать по убыванию следующего выражения: length / rental_duration.

```sql
select
	length,
	rental_duration,
	title
from
	film
order by
	length / rental_duration desc;
```

3.Из таблицы фильмов (film) запросить все поля с помощью *. Отсортировать полученный набор сначала по рейтингу (rating) по возрастанию, а фильмы с одинаковым рейтингом по убыванию продолжительности (length).

```sql
select
	*
from
	film f
order by
	rating,
	length desc;
```
