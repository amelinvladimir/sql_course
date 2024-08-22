# Разбор домашнего задания 11.2
Оптимизируйте запрос с помощью создания индекса:
```sql
select
        *
from
        film f
where rental_duration = 7;
```
Постройте план выполнения запроса до создания индекса и после и посмотрите на сколько изменится время выполнения запроса.
```sql
explain analyze
select
	*
from
	film f
where
	rental_duration = 7;
```
```sql
create index film_rental_duration_idx on
film(rental_duration);
```


