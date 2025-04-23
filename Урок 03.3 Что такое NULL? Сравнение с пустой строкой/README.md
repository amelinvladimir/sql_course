# Что такое NULL? Сравнение с пустой строкой.

```sql
select 1, 5+6, 1=6;
```

```sql
select null = 'Some string';
select '' = 'Some string';
```

```sql
select null || 'Some string';
select '' || 'Some string';
```

```sql
select
	*
from
	address
where
	address2 <> 'Moscow';
```

```sql
select
	*
from
	address a
where
	address2 <> 'Moscow'
	or address2 is null;
```

```sql
select
	*
from
	address a
where
	address2 = null;
```

```sql
select '' = '';
select null = null;
select null = '';
select 1=1 and null = '';
select 1=1 or null = '';
```

```sql
select
	*
from
	address a
where
	address2 in ('Moscow', '', null);
```

