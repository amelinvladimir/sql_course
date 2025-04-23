# Разбор домашнего задания 4.1
1.Нам известно название фильма (значение поля title таблицы film) - "Chamber Italian".
Задача: получить список всех актеров, снявшихся в этом фильме.
По каждому актеру (запись из таблица actor) нужно вывести 2 поля:
имя (first_name) и фамилию (last_name).Связь между таблицами фильмов и актером производится посредствам 
промежуточной таблицы film_actor  
```sql
select
	a.first_name ,
	a.last_name
from
	film f
inner join film_actor fa 
on
	fa.film_id = f.film_id
inner join actor a 
on
	a.actor_id = fa.actor_id
where
	f.title = 'chamber italian';

```
```sql
select
	a.first_name ,
	a.last_name
from
	film f
join film_actor fa
		using (film_id)
join actor a
		using (actor_id)
where
	f.title = 'chamber italian';

```
2.Получить список всех фильмов (film) из категории (category) 'Comedy' 
(значение поля "name"). По каждому найденному фильму нужно вывести название из поля "title". 
Связь между фильмами и категориями осуществляется с помощью промежуточной таблицы film_category.
```sql
select
	f.title
from
	category c
join film_category fc 
on
	fc.category_id = c.category_id
join film f 
on
	fc.film_id = f.film_id
where
	c."name" = 'comedy';

```
3.Вывести список пар: 
название фильма (film.title) - название категории (category.name).
если один фильм попадает в несколько категорий, то вывести несколько строк для этого фильма.
Связь между таблицами фильмов (film) и категорий (category)
осуществляется посредствам промежуточной таблицы film_category. 
```sql
select
	f.title,
	c."name"
from
	film f
join film_category fc 
on
	f.film_id = fc.film_id
join category c 
on
	c.category_id = fc.category_id;
```
*Вывести список всех пар: название фильма (film.title) и 
название категории (category.name).
Для каждой пары вывести true в 3ьей колонке, если данный фильм 
относится к указанной категории. иначе вывести false. 
```sql
select
	f.title,
	c."name",
	fc.film_id is not null
from
	film f
cross join category c
left join film_category fc 
on
	fc.film_id = f.film_id
	and fc.category_id = c.category_id 
```
```sql
select
	f.title,
	c."name"
from
	film f
inner join category c on
	true
```
```sql
select
	f.title,
	c."name"
from
	film f,
	category c 
```
*Вывести названия всех фильмов (film.title), по которым в магазине нет дисков и кассет (то есть по таким фильмам нет записей в таблице inventory). 
```sql
select
	f.title
from
	film f
left join inventory i 
on
	i.film_id = f.film_id
where
	i.film_id is null;
```
