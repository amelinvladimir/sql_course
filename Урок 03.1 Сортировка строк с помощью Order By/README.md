# Сортировка строк с помощью Order By

```sql
select
	*
from
	actor
order by
	first_name;
```

```sql
select
	*
from
	actor
order by
	first_name,
	last_name;
```

```sql
select
	*
from
	actor
where
	first_name like '%a%'
order by
	first_name,
	last_name;
```

```sql
select
	*
from
	actor
order by
	first_name desc,
	last_name;
```

```sql
select
	*
from
	actor
order by
	first_name || last_name,
	mod(actor_id, 10);
```

```sql
select
	*
from
	actor
order by
	mod(actor_id, 10);
```

```sql
select
	first_name f,
	last_name l,
	actor_id i
from
	actor
order by
	f, l;
```

```sql
select
	last_name l,
	first_name f,
	actor_id i
from
	actor
order by
	1, 2;
```

```sql
select
	*
from
	address a
order by
	address2 desc nulls last;
```

```sql
select
	*
from
	staff s
order by
	picture nulls first;
```
