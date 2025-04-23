# Получение уникальных значений. Distinct

```sql
select distinct 
	rental_rate
from
	film;
```

```sql
select distinct
	last_name,
	first_name
from
	actor;
```

```sql
select distinct
	substring(last_name, 1, 3)
from
	actor;
```

```sql
select distinct on (rental_rate)
	rental_rate,
	title
from
	film;
```

```sql
select distinct on (inventory_id)
	rental_id,
	rental_date,
	inventory_id,
	customer_id,
	return_date,
	staff_id,
	last_update
from
	rental
order by
	inventory_id,
	rental_date desc;
```

```sql
select
	rental_id,
	rental_date,
	inventory_id,
	customer_id,
	return_date,
	staff_id,
	last_update
from
	rental
where
	inventory_id = 1;
```

```sql
select distinct on (staff_id)
	staff_id,
	amount
from
	payment
order by
	staff_id,
	amount desc;
```
