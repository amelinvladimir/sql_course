# Разбор домашнего задания 8.1
1.Вывести список всех фильмов (film). По каждому фильму отобразить поля:
- название (film.title).
- кол-во дней, на которые фильм дается в аренду (film.rental_duration).
- общее кол-во фильмов, которые даются в аренду на такое же кол-во дней (с таким же значением film.rental_duration)
```sql
select
	f.title,
	f.rental_duration,
	count(*) over(partition by f.rental_duration) as rental_dur_cnt
from
	film f;
```
2.Вывести список всех фильмов (film). По каждому фильму отобразить поля:
- название (film.title).
- кол-во дней, на которые фильм дается в аренду (film.rental_duration).
- продолжительность фильма (film.length).
- порядковый номер фильма в порядке уменьшения продолжительности (film.length).
  Нумеруем в рамках групп фильмов с одинаковым значением film.rental_duration. 
У каждого фильма должен быть свой уникальный номер. Фильмы с одинаковой продолжительностью сортируем по названию (film.title) в алфавитном порядке.
```sql
select
	f.title,
	f.rental_duration,
	f.length,
	row_number() over(partition by f.rental_duration
order by
	f.length desc,
	f.title) as rn
from
	film f;
```
3.*На основе таблицы платежей (payment) посчитать накопительным итогом общую сумму платежей (sum(payment.amount)) на каждую дату, на которую были платежи. Вывести поля:
- дата (payment.payment_date::date). Одну дату выводим в одной строке.
- общая сумма всех платежей (sum(payment.amount)) за все даты до текущей, а также за текущую дату.
```sql
with payment_date as (
	select
		p.payment_date::date as pay_date,
		sum(p.amount) as amount
	from
		payment p
	group by
		p.payment_date::date

)

select
	p.pay_date,
	sum(p.amount) over(
	order by p.pay_date) as cumulative_amount
from
	payment_date p;
```
```sql
select
	p.payment_date::date as pay_date,
	sum(sum(p.amount)) over(
	order by p.payment_date::date) as amount
from
	payment p
group by
	p.payment_date::date;
```
Задание для повторения и закрепления пройденных тем

Запросите адреса клиентов проката с индексом(postal_code), начинающимся на 6 ,а также необходимо включить адреса в городе (city.city) Лондон. 
В итоговую таблицу выведите индекс(postal_code), адрес (address). Используйте union, join, like.
```sql
select
	postal_code,
	address
from
	address a
where
	postal_code like '6%'
union  

select
	postal_code,
	address
from
	address a
join city c
		using (city_id)
where
	city = 'london';
```
