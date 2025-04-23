# Разбор домашнего задания 7.2
По каждому фильму (film) вывести поля:
- название фильма (film.title).
- кол-во актеров, снявшихся в фильме (кол-во строк в film_actor).
- сумму продаж по данному фильму (sum(payment.amount)).
Сделать расчет кол-ва актеров в каждом фильме в отдельном запросе cte.  Сделать расчет общей суммы продаж по каждому фильму в отдельном cte.

```sql

with film_actor_cnt as (
select
	fa.film_id,
	count(*) as cnt
from
	film_actor fa
group by
	fa.film_id

),

film_amount as (
select
	i.film_id,
	sum(p.amount) as amount
from
	inventory i
join rental r 

on
	i.inventory_id = r.inventory_id
join payment p 

on
	p.rental_id = r.rental_id
group by
	i.film_id

)

select
	f.title,
	coalesce(fa.cnt, 0) as film_actor_cnt,
	coalesce(fam.amount, 0) as amount
from
	film f
left join film_actor_cnt fa

on
	f.film_id = fa.film_id
left join film_amount fam

on
	f.film_id = fam.film_id;
```
Вывести по каждому фильму (film):
- название (film.title).
- общую сумму продаж по фильму (sum(payment.amount)).
- общую сумму продаж по всем фильмам (sum(payment.amount)).
- долю продаж данного фильма от всех продаж в процентах, рассчитанную по формуле: [продажи по данному фильму] / [продажи по всем фильмам] * 100.
 Расчет всех продаж по всем фильмам сделать с помощью CTE.
```sql
with film_amount as (
select
	i.film_id,
	sum(p.amount) as amount
from
	inventory i
join rental r 

on
	i.inventory_id = r.inventory_id
join payment p 

on
	p.rental_id = r.rental_id
group by
	i.film_id

),

total_amount as (
select
	sum(fa.amount) as total_amount
from
	film_amount fa

)

select
	f.title,
	coalesce(fa.amount, 0) as amount,
	ta.total_amount,
	coalesce(fa.amount, 0) / ta.total_amount * 100 as percent_amount
from
	film f
left join film_amount fa

on
	fa.film_id = f.film_id
cross join total_amount ta;
```
