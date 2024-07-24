# Функции работы со строками

```sql
select
	first_name,
	last_name,
	concat(first_name, ' ', last_name),
	first_name || ' ' || last_name,
	trim(leading from ' ' || first_name || ' '),
	substring(first_name || ' ' || last_name, 3, 10),
	char_length(first_name),
	upper(first_name),
	lower(first_name),
	trim('er' from first_name)
from
	actor;
```

```sql
select
	email,
	substring(email, 1, strpos(email, '@') - 1),
	strpos(email, '@'),
	substring(email, strpos(email, '@') + 1)
from
	staff;
```
