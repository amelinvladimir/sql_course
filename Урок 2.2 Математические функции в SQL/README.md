# Математические функции в SQL

```sql
select
	amount,
	amount + 2,
	amount - 3,
	amount * 1.5,
	amount / 3,
	amount ^ 2,
	amount % 4,
	mod(amount,
	4),
	amount / 2,
	div(amount,
	2),
	round(amount / 2,
	1),
	floor(amount / 2),
	ceil(amount / 2)
from
	public.payment;

```
