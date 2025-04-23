# Урок 2.1 Разбор домашнего задания

1. Сделать запрос из таблицы платежей (payment), который получает поля: 
payment_id, customer_id, amount 
и дать им названия соответственно: 
“№ платежа”, “№ покупателя” и “Сумма платежа”.
```sql
select
	payment_id as "№ платежа",
	customer_id as "№ покупателя",
	amount as "Сумма платежа"
from
	payment;

```

2. Вывести по каждому платежу их таблицы платежей (payment) сумму платежа в долларах (значение из поля amount) и сумму платежа в рублях (значение из поля amount, умноженное на текущий курс доллара к рублю) и дать им названия: “Сумма в долларах” и “Сумма в рублях”.
```sql
select
	amount as "Сумма в долларах",
	amount * 71 as "Сумма в рублях"
from
	payment;
```

3. Сделать запрос из таблицы фильмов (film) со следующими столбцами:

Для каждого фильма вывести строку в следующем формате: 

“title: {1}; description: {2}”, 
где вместо {1} будет настоящее название фильма, 
а вместо {2} - описание фильма. 

Например, для фильма с названием “Chamber Italian” и описанием 
“A Fateful Reflection of a Moose And a Husband who must Overcome a Monkey in Nigeria” 
нужно вывести строку: “title: Chamber Italian; description: A Fateful Reflection of a Moose And a Husband who must Overcome a Monkey in Nigeria”. Дать название столбцу: fullTitle.

Вывести описание фильма (film.description), у которого удалена подстрока “A ” из начала строки, если такая есть. 
Дать название полученному столбцу: trimmedDescription.
Из названия фильма вывести только первое слово, которое идет до пробела. 
Например, для фильма с названием “Chamber Italian” нужно вывести “Chamber”. 
Дать название полученному столбцу: titleFirstWord.

```sql
select
	concat('title: ', title, '; description: ', description) as fullTitle,
	trim('A ' from description) as trimmedDescription,
	substring(title, 1, strpos(title, ' ') - 1) as titleFirstWord
from
	film;
```

```sql
select
	trim(trailing ' ' || first_name || ' ') as trimmedFirstName,
	rtrim(' ' || first_name || ' ') rtrimmed
from
	actor;
```
