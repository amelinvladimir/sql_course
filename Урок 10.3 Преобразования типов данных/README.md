# Преобразования типов данных
```sql
select
	f.rental_rate,
	cast(f.rental_rate as varchar(10))
from
	film f;
```
```sql
select
	1 as filed1
union all
select
	1.5 as filed1;
```
```sql
with cte as (
	select
		1 as filed1
union all
	select
		1.5 as filed1

)

select
	filed1,
	pg_typeof(filed1)
from
	cte;
```
```sql
select
	cast(1 as numeric) as filed1
union all

select
	1.5 as filed1;
```
```sql
select
	1::numeric as filed1
union all
select
	1.5 as filed1;
```
```sql
with cte as (
select
	1 as filed1
union all
select
	1 as filed1
)
select
	filed1,
	pg_typeof(filed1)
from
	cte;
```
```sql
select
	1 as filed1
union all

select
	'2' as filed1;
```
```sql
select
	1 as filed1
union all
select
	'some text' as filed1;
```
```sql
select
	cast(1 as varchar) as filed1
union all
select
	'2' as filed1;
```
```sql
select
	1 as field1
union all
select
	false as field1;
```
```sql
select
	now();
```
```sql
select
	to_char(now(), 'yyyy---mm---dd  hh:mi');
```
```sql
select
	to_char(now(), 'dd/mm/yyyy');
```
```sql
select
	to_char(now(), 'dd/mon/yyyy');
```
```sql
select
	to_char(now(), 'dd/month/yy hh24:mi:ss');
```
```sql
select
	cast('2021-10-01' as date);
```
```sql
select
	cast('01/10/2021 10:21' as timestamp);
```
```sql
select
	to_date('21/10/01', 'yy/mm/dd');
```
```sql
select
	to_timestamp('21/10/01 10:11', 'yy/mm/dd hh24:mi');
```
