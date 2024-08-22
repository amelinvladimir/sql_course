# Ограничения
```sql
drop table internet_customer;
```
```sql
create table internet_customer (
customer_id serial not null,
login varchar(20) not null,
first_name character(20) not null,
last_name character(20) not null,
patronymic character varying(20) null,
rating float default(0) not null,
birthday date null
);
```
```sql
insert
	into
	public.internet_customer
(login,
	first_name,
	last_name,
	patronymic,
	birthday)
values
('login1',
'ivan',
'petrov',
null,
'1987-01-03'),

('login2',
'petr',
'ivanov',
'makarovich',
'1991-10-11'),

('login3',
'сергей',
'иванов',
'андреевич',
'1995-11-02');
```
```sql
select
	*
from
	internet_customer;
```
```sql
drop table internet_customer;
```
```sql
create table internet_customer (
customer_id serial not null,
login varchar(20) not null check(length(login) >= 6),
first_name character(20) not null,
last_name character(20) not null,
patronymic character varying(20) null,
rating float default(0) not null constraint internet_customer_rating check(rating >= 0),
birthday date null
);
```
```sql
insert
	into
	public.internet_customer
(login,
	first_name,
	last_name,
	patronymic,
	birthday)
values
('login1',
'ivan',
'petrov',
null,
'1987-01-03'),
('login2',
'petr',
'ivanov',
'makarovich',
'1991-10-11'),
('login3',
'сергей',
'иванов',
'андреевич',
'1995-11-02');
```

```sql
drop table internet_customer;
```
```sql
create table internet_customer (
customer_id serial not null,
login varchar(20) not null check(length(login) >= 6
and login <> first_name
and login <> last_name),
first_name character(20) not null,
last_name character(20) not null,
patronymic character varying(20) null,
rating float default(0) not null constraint internet_customer_rating check(rating >= 0),
birthday date null
);
```
```sql
insert
	into
	public.internet_customer

(login,
	first_name,
	last_name,
	patronymic,
	birthday)
values

('login1',
'ivan',
'petrov',
null,
'1987-01-03'),

('login2',
'petr',
'ivanov',
'makarovich',
'1991-10-11'),

('login3',
'сергей',
'иванов',
'андреевич',
'1995-11-02');
```
```sql
drop table internet_customer;
```
```sql
create table internet_customer (
customer_id serial not null,
login varchar(20) not null,
first_name character(20) not null,
last_name character(20) not null,
patronymic character varying(20) null,
rating float default(0) not null,
birthday date null,
check(length(login) >= 6
and login <> first_name
and login <> last_name),
constraint internet_customer_rating check(rating >= 0)
);
```
```sql
drop table internet_customer;
```
```sql
create table internet_customer (
customer_id serial not null,
login varchar(20) not null,
first_name character(20) not null,
last_name character(20) not null,
patronymic character varying(20) null,
rating float default(0) not null,
birthday date null,
check(length(login) >= 6
and login <> first_name
and login <> last_name
and rating >= 0)
);
```
```sql
drop table internet_customer;
```
```sql
create table internet_customer (
customer_id serial not null,
login varchar(20) not null unique,
first_name character(20) not null,
last_name character(20) not null,
patronymic character varying(20) null,
rating float default(0) not null,
birthday date null,
check(length(login) >= 6
and login <> first_name
and login <> last_name
and rating >= 0),
constraint internet_customer_unique_fi unique(first_name,
last_name)
);
```
```sql
insert
	into
	public.internet_customer

(login,
	first_name,
	last_name,
	patronymic,
	birthday)
values

('login1',
'ivan',
'petrov',
null,
'1987-01-03'),

('login2',
'ivan',
'sergeev',
'makarovich',
'1991-10-11'),

('login3',
'сергей',
'иванов',
'андреевич',
'1995-11-02');
```
```sql
drop table internet_customer;
```
```sql
create table internet_customer (
customer_id serial primary key,
login varchar(20) not null unique,
first_name character(20) not null,
last_name character(20) not null,
patronymic character varying(20) null,
rating float default(0) not null,
birthday date null,
check(length(login) >= 6
and login <> first_name
and login <> last_name
and rating >= 0),
constraint internet_customer_unique_fi unique(first_name,
last_name)
);
```
```sql
drop table internet_customer;
```
```sql
create table internet_customer (
login varchar(20) primary key,
first_name character(20) not null,
last_name character(20) not null,
patronymic character varying(20) null,
rating float default(0) not null,
birthday date null,
check(length(login) >= 6
and login <> first_name
and login <> last_name
and rating >= 0),
constraint internet_customer_unique_fi unique(first_name,
last_name)
);
```
```sql
insert
	into
	public.internet_customer

(login,
	first_name,
	last_name,
	patronymic,
	birthday)
values

('login1',
'ivan',
'petrov',
null,
'1987-01-03'),

('login2',
'ivan',
'sergeev',
'makarovich',
'1991-10-11'),

('login3',
'сергей',
'иванов',
'андреевич',
'1995-11-02');
```
```sql
drop table internet_customer;
create table internet_customer (
login varchar(20) not null unique,
first_name character(20) not null,
last_name character(20) not null,
patronymic character varying(20) null,
rating float default(0) not null,
birthday date null,
check(length(login) >= 6
and login <> first_name
and login <> last_name
and rating >= 0),
constraint internet_customer_unique_fi unique(first_name,
last_name),
primary key(first_name,
last_name)
);
```
```sql
insert
	into
	public.internet_customer

(login,
	first_name,
	last_name,
	patronymic,
	birthday)
values

('login1',
'ivan',
'petrov',
null,
'1987-01-03'),

('login2',
'ivan',
'sergeev',
'makarovich',
'1991-10-11'),

('login3',
'сергей',
'иванов',
'андреевич',
'1995-11-02');

```
```sql
select
	*
from
	internet_customer;
```
```sql
create table internet_order (
internet_order_id serial primary key,
internet_customer_id int references internet_customer(customer_id),
film varchar(50)
);
```
```sql
insert
	into
	internet_order

(internet_customer_id,
	film)
values 

(1,
'some film');
```
```sql
select
	*
from
	internet_order;
```
```sql
insert
	into
	internet_order
(internet_customer_id,
	film)
values 
(4,
'some film');
```
