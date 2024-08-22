# Разбор домашнего задания 3.2

1.Получить список уникальных значений из колонки продолжительности сдачи в аренду (rental_duration) таблицы с фильмами (film)

```sql
select distinct
	rental_duration
from
	film;
```

2.Из таблицы актеров (actor) у имени (first_name) каждого актера берем только первые три символа. 
Выводим один столбец с уникальными значениями полученного выражения. 


```sql
select distinct
	substring(first_name, 1, 3)
from
	actor;
```

3.Из таблицы платежей (payment) получить для каждого покупателя (customer_id) последний платеж по дате платежа (payment_date). 
Вывести поля: 
номер платежа (payment_id), 
номер покупателя (customer_id), 
сумму платежа (amount), 
дату платежа (payment_date). 

```sql
select distinct on (customer_id)
	payment_id,
	customer_id,
	amount,
	payment_date
from
	payment
order by
	customer_id,
	payment_date desc;
```
