# Разбор домашнего задания 9.1
1.Создать таблицу (internet_film) со списком фильмов, доступных для аренды онлайн.
Список полей:
- internet_film_id - Идентификатор фильма (целое число. Должно проставляться автоматически. Обязательное для заполнения).
- title - Название фильма (строка длиной до 50 символов. Пробелами в конце дополняться не должна. Обязательное для заполнения).
- price - Стоимость сдачи в прокат (число с плавающей точкой. Обязательное для заполнения).
- rental_duration - Кол-во дней, на которое фильм отдается в прокат (Целое число. Обязательное для заполнения).
- description - Описание фильма (строка длиной до 500 символов. Не обязательное для заполнения).

```sql
create table internet_film (
internet_film_id serial not null,
title varchar(50) not null,
price numeric(10,
2) not null,
rental_duration smallint not null,
description varchar(500) 
);
```
```sql
select
	*
from
	internet_film;
```
2.Добавить в таблицу 3 любых фильма по своему желанию.
```sql
insert
	into
	internet_film

(title,
	price,
	rental_duration,
	description)
values 

('titanik',
2,
2,
'romantic story'),

('james bond part 1',
3,
2,
'adventure'),

('shrek',
3,
3,
'for children');

```
```sql
select
	*
from
	internet_film;
 ```
3.Добавить в таблицу все фильмы из таблицы film, у которых рейтинг ‘G’ (ilm.rating = ‘G’). Поставить цену проката - 2. Остальные поля взять из таблицы film.
```sql
insert
	into
	internet_film

(title,
	price,
	rental_duration,
	description)
```
```sql
select
	f.title,
	2,
	f.rental_duration,
	f.description
from
	film f
where
	f.rating = 'g';
```
```sql
select * from internet_film;
```
