# Разбор домашнего задания 10.1
1.Задача: создать представление, в котором будет 2 поля:
- film_id - идентификатор фильма
- actor_cnt - кол-во актеров, снявшихся в фильме
Если в фильме не снялось ни одного актера, то такой фильм должен выводится в этом представлении с 0 актеров.
```sql
create view film_actor_cnt as
select
	f.film_id,
	count(fa.film_id) as actor_cnt
from
	film f
left join film_actor fa 
on
	f.film_id = fa.film_id
group by
	f.film_id;
```
```sql
select
	*
from
	film_actor_cnt;
```
2.Написать запрос, в котором будет использовано представление из предыдущей задачи. Вывести список всех фильмов (film) и по каждому фильму отобразить:
- название фильма (film.title)
- кол-во актеров, снявшихся в фильме
```sql
select
	f.title,
	fa.actor_cnt
from
	film f
inner join film_actor_cnt fa
on
	f.film_id = fa.film_id;
```
3.Удалить представление, созданное в первой задаче.
```sql
drop view film_actor_cnt;
```


