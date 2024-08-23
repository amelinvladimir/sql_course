# Разбор домашнего задания 11.1
1.Для сотрудника с идентификатором 2 посчитать, сколько всего у него подчиненных.
```sql
with recursive subordinates as (
-- select 
-- e.employee_id 
-- from 
-- employees e 
-- where 
-- e.employee_id = 2
select
	2 as employee_id
union
select
	e.employee_id
from
	subordinates s
join employees e 
on
	e.manager_id = s.employee_id
)
select
	count(*) - 1 as subordinates_cnt
from
	subordinates;
```
2.Для сотрудника с идентификатором 20 посчитать, сколько всего у него начальников.
```sql
with recursive managers as (
select
	e.manager_id
from
	employees e
where
	e.employee_id = 20
union
select
	e.manager_id
from
	managers m
join employees e 
on
	e.employee_id = m.manager_id
)
select
	count(manager_id)
from
	managers;
```
3.* С помощью рекурсивного запроса вывести сотрудника с идентификатором 1 и всех его подчиненных со второго и третьего уровней иерархии.
 С 4ого уровня и ниже подчиненных выводить не нужно.
```sql
with recursive subordinates as (
select
	e.employee_id,
	e.full_name,
	1 as level_hier
from
	employees e
where
	e.employee_id = 1
union
select
	e.employee_id,
	e.full_name,
	s.level_hier + 1 as level_hier
from
	subordinates s
join employees e 
on
	e.manager_id = s.employee_id
where
	s.level_hier + 1 < 4
)
select
	e.employee_id,
	e.full_name
from
subordinates e;
```


