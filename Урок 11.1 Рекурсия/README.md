# Рекурсия

```sql
def factorial(x):
   print("x=" + str(x))
   if x == 1:
       return 1
else:
       return factorial(x-1) * x


print(factorial(3))
```
```sql
drop table if exists employees;
```
```sql
create table employees (
employee_id serial primary key,
full_name varchar not null,
manager_id int
);
```
```sql
insert
	into
	employees (

employee_id,
	full_name,
	manager_id

)
values

(1,
'michael north',
null),

(2,
'megan berry',
1),

(3,
'sarah berry',
1),

(4,
'zoe black',
1),

(5,
'tim james',
1),

(6,
'bella tucker',
2),

(7,
'ryan metcalfe',
2),

(8,
'max mills',
2),

(9,
'benjamin glover',
2),

(10,
'carolyn henderson',
3),

(11,
'nicola kelly',
3),

(12,
'alexandra climo',
3),

(13,
'dominic king',
3),

(14,
'leonard gray',
4),

(15,
'eric rampling',
4),

(16,
'piers paige',
7),

(17,
'ryan henderson',
7),

(18,
'frank tucker',
8),

(19,
'nathan ferguson',
8),

(20,
'kevin rampling',
8);

```
```sql
select
	*
from
	employees;
```
```sql
with recursive subordinates as (
select
	e.employee_id,
	e.full_name
from
	employees e
where
	e.employee_id = 2
union
select
	e.employee_id,
	e.full_name
from
	subordinates s
join employees e 

on
	s.employee_id = e.manager_id
)
select
	*
from
	subordinates;
```
```sql
with recursive managers as (
	select
		e.employee_id,
		e.full_name,
		e.manager_id
	from
		employees e
	where
		e.employee_id = 18
union all
	select
		e.employee_id,
		e.full_name,
		e.manager_id
	from
		managers m
	join employees e

on
		e.employee_id = m.manager_id
)
select
	*
from
	managers;
```
      - 1 этап
      
```sql
select
	e.employee_id,
	e.full_name,
	e.manager_id
from
	employees e
where
	e.employee_id = 18;
```
  - Результат выполнения запроса
	- 18 frank tucker 8
	- общий результат выполнения cte 
	- 18 frank tucker 8
	- содержимое managers
	- 18 frank tucker 8
      - 2 этап
```sql
select
	e.employee_id,
	e.full_name,
	e.manager_id
from
	managers m
join employees e
on
	e.employee_id = m.manager_id;
```
  - результат выполнения запроса
	- 8 max mills 2
	- общий результат выполнения cte 
	- 18 frank tucker 8
	- 8 max mills 2
	- содержимое managers
	- 8 max mills 2
      - 3 этап

```sql
select
	e.employee_id,
	e.full_name,
	e.manager_id
from
	managers m
join employees e
on
	e.employee_id = m.manager_id;
```
- результат выполнения запроса
	- 2 megan berry 1
	- общий результат выполнения cte 
	- 18 frank tucker 8
	- 8 max mills 2
	- 2 megan berry 1
	- содержимое managers
	- 2 megan berry 1
      - 4 этап
```sql
select
	e.employee_id,
	e.full_name,
	e.manager_id
from
	managers m
join employees e
on
	e.employee_id = m.manager_id;
```
- результат выполнения запроса
	- 1 michael north
	- общий результат выполнения cte 
	- 18 frank tucker 8
	- 8 max mills 2
	- 2 megan berry 1
	- 1 michael north
	- содержимое managers
	- 1 michael north
      - 5 этап
```sql
select
	e.employee_id,
	e.full_name,
	e.manager_id
from
	managers m
join employees e
on
	e.employee_id = m.manager_id;
```
- результат выполнения запроса
	- общий результат выполнения cte 
	- 18 frank tucker 8
	- 8 max mills 2
	- 2 megan berry 1
	- 1 michael north
```sql
with recursive factorial as (
	select
		1 as n,
		1 as res
union
	select
		f.n + 1 as n,
		f.res * (f.n + 1) as res
	from
		factorial f
	where
		f.n + 1 <= 5
)
select
	*
from
	factorial;
```
```sql
with recursive factorial as (
select
	5 as n,
	5 as res
union
select
	f.n - 1 as n,
	f.res * (f.n - 1) as res
from
	factorial f
where
	f.n - 1 >= 1
)
select
	*
from
	factorial
where
	n = 1;
```
