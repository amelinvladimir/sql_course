# Урок 5.2 Разбор домашнего задания 
Написать запрос, который возвращает 2 колонки:
1. имя и фамилию актера через пробел.
2. кол-во фильмов, в которых снялся актер.
Нужно вывести вторую пятерку актеров (пять актеров, начиная с шестого) в порядке убывания кол-ва фильмов, в которых они снимались.
```sql
select
	a.first_name || ' ' || a.last_name as actor_name,
	count(*) as film_cnt
from
	actor a
left join film_actor fa 
on
	a.actor_id = fa.actor_id
group by
	actor_name,
	a.actor_id
order by
	film_cnt desc,
	actor_name
limit 5
offset 5;
```
