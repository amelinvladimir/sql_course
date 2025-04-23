# Получение столбцов и их именование в select

```sql
select
	actor_id actorIdentity,
	first_name as firstName,
	last_name "Last Name",
	last_update as "Last Update"
from
	actor;
```
