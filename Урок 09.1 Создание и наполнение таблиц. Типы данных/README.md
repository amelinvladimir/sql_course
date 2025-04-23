# Создание и наполнение таблиц. Типы данных

```sql
drop table internet_customer;
```
```sql
create table internet_customer (
internet_customer_id int not null,
login varchar(20) not null,
first_name varchar(20) not null,
last_name varchar(20) not null,
patronymic varchar(20) null,
rating float default(0) not null,
birthday date null,
registered timestamp default(now()) not null,
deleted bool default(false) not null
);
```
-select * from internet_customer;
- smallint  2 байта   -32 768..32 767
- int       4 байта   -2 147 483 648..2 147 483 647
- bigint    8 байт    -9 223 372 036 854 775 808..9 223 372 036 854 775 807
- character  char
- character varying  varchar
- text
- float float4 real  4 байта
- double precision, float8  8 байт
- numeric(n, m), decimal(n, m)   1 234 567.890   numeric(15, 5)
- date
- timestamp 
- time
- interval 
-bool

```sql
insert
	into
	internet_customer
(internet_customer_id,
	login,
	first_name,
	last_name,
	patronymic,
	birthday)
values 
(1,
'login1',
'иван',
'петров',
'александрович',
'1987-01-05'),
(2,
'login2',
'петр',
'иванов',
null,
'1991-11-06'),
(3,
'login3',
'mark',
'stevens',
null,
'1995-12-16');
```
```sql
select
	*
from
	internet_customer;
```
```sql
insert
	into
	internet_customer
(login,
	internet_customer_id)
values 
('login1',
1),

('login2',
2),

('login3',
3);
```
```sql
alter table internet_customer add column confirmed bool default(false) not null;
```
```sql
alter table internet_customer drop column confirmed;
```
```sql
alter table internet_customer add column confirmed bool null;
```
```sql
select
	*
from
	internet_customer;
```
```sql
insert
	into
	internet_customer
(internet_customer_id,
	login,
	first_name,
	last_name,
	patronymic,
	birthday)


select
	row_number() over() + 3,
	substring(first_name, 1, 1) || '.' || last_name,
	a.first_name,
	a.last_name,
	null,
	null
from
	actor a;
```
```sql
insert
	into
	internet_customer

select
	row_number() over() + 3,
	substring(first_name, 1, 1) || '.' || last_name,
	a.first_name,
	a.last_name,
	null,
	0,
	null,
	now(),
	false
from
	actor a;
```
```sql
drop table internet_customer;
```
```sql
create table internet_customer (
internet_customer_id serial not null,
login varchar(20) not null,
first_name varchar(20) not null,
last_name varchar(20) not null,
patronymic varchar(20) null,
rating float default(0) not null,
birthday date null,
registered timestamp default(now()) not null,
deleted bool default(false) not null
);
```
```sql
insert
	into
	internet_customer
(login,
	first_name,
	last_name,
	patronymic,
	birthday)

select
	substring(first_name, 1, 1) || '.' || last_name,
	a.first_name,
	a.last_name,
	null,
	null
from
	actor a;
```
```sql
insert
	into
	internet_customer
(login,
	first_name,
	last_name,
	patronymic,
	birthday)
values 
('login1',
'иван',
'петров',
'александрович',
'1987-01-05'),
('login2',
'петр',
'иванов',
null,
'1991-11-06'),

('login3',
'mark',
'stevens',
null,
'1995-12-16');
```
```sql
delete
from
	internet_customer
where
	last_name = 'петров';
```
```sql
update
	internet_customer
set
	login = 'testlogin'
where
	last_name = 'stevens';
```
```sql
select
	*
from
	internet_customer;
```


