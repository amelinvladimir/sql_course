# Разбор домашнего задания 4.2
1. По каждому фильму (film), по которому были платежи, вывести общую сумму вырученных платежей (payment.amount) с проката. 
 Вывести 2 колонки: 1) film_title - с названием фильма (film.title). Каждый фильм, должен быть указан в этой колонке один раз; 2) amount - общая сумма, на которую фильм сдавался в прокат (payment.amount). 
Отсортировать полученный результат в порядке убывания общей суммы сдачи в прокат. 
Связь таблиц происходит следующим образом: film <- inventory; inventory <- rental; rental <- payment.
```sql
select 
	f.title,
	sum(p.amount) as amount
from 
	film f
join inventory i 
		on
	i.film_id = f.film_id
join rental r 
		on
	r.inventory_id = i.inventory_id
join payment p 
		on
	p.rental_id = r.rental_id
group by 	
	f.title
order by 
	amount desc;
```
2. По каждому актеру (actor) вывести в скольких фильмах он снимался. Вывести 2 колонки в результате: 1) actor_name - имя (actor.first_name) и фамилия (actor.last_name) актера через пробел; 2) film_number - кол-во фильмов (film), в которых снимался актер. 
Отобразить только актеров, которые снялись более чем в 20 фильмах.
```sql
select 
	a.first_name || ' ' || a.last_name as actor_name,
	count(*) as film_number
from 
	actor a
join film_actor fa 
		on
	a.actor_id = fa.actor_id
group by 
	actor_name
having 
	count(*) > 20;
```
3. Вывести одно число - сколько всего фильмов (film) продолжительностью (film.length) более 120 минут.
```sql
select 
	count(*)
from 
	film f
where 
	f.length > 120;
```
* По каждой категории фильмов (category) вывести кол-во фильмов (film) продолжительностью (film.length) от 180 минут.
Вывести 2 поля: 1) category_name - название категории (category.name), 2) film_number - кол-во фильмов продолжительностью от 180 минут.
Если в категории нет фильмов продолжительностью от 180 минут - ее также нужно отобразить, но в film_number для нее нужно вывести 0. 
Отсортировать результат по убыванию кол-ва фильмв в категории. 
```sql
select 
	c."name" as category_name,
	count(f.film_id) as film_number
from 
	category c
left join film_category fc 
		on
	c.category_id = fc.category_id
left join film f
		on
	f.film_id = fc.film_id
	and f.length >= 180
group by 
	c."name"
order by 
	film_number desc;
```
