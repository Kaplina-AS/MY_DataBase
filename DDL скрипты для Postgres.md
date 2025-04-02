# DDL скрипты для Postgres
## Создание базы данных

>Создание БД
![Результат 1](/DataBase/create_database.png)
>Результат создания БД
![Результат 2](/DataBase/db.png)
> Создание табличного пространства и ролей
![Результат 3](/DataBase/1.png)
![Результат 33](/DataBase/role.png)
>Создание схемы БД
![Результат 4](/DataBase/schema.png)

## Создание таблиц БД
**Таблица клиенты**
```
 CREATE TABLE beaty_salon.clients
(
    client_id SERIAL PRIMARY KEY NOT NULL,
    last_name varchar(255) NOT NULL,
    first_name varchar(255) NOT NULL,
	middle_name varchar(255),
    birth_date date,
	phone varchar(20),
	email varchar(50),
	created_at timestamp NOT NULL,
	updated_at timestamp NOT NULL
);
 ```
 **Таблица Cотрудники**
```
 CREATE TABLE beaty_salon.services
(
   service_id SERIAL PRIMARY KEY NOT NULL,
    service_name varchar(100) NOT NULL,
	description varchar(255),
	category_id serial references beaty_salon.service_category(category_id),
	duration int4 NOT NULL,
	price numeric NOT NULL,
	notes text,
	created_at timestamp NOT NULL,
	updated_at timestamp NOT NULL
);
 ```
 **Таблица Специализации сотрудников**
```
 CREATE TABLE beaty_salon.specialization
(
   specialization_id SERIAL PRIMARY KEY NOT NULL,
    specialization_name varchar(255) NOT NULL,
    description varchar(255),
	notes text,
	created_at timestamp NOT NULL,
	updated_at timestamp NOT NULL
);
 ```
**Таблица Категории услуг**
```
CREATE TABLE beaty_salon.service_category
(
    category_id SERIAL PRIMARY KEY NOT NULL,
    category_name varchar(255) NOT NULL,
    description varchar(255) NOT NULL,
	created_at timestamp NOT NULL,
	updated_at timestamp NOT NULL
);
 ```
 **Таблица Услуги**
```
CREATE TABLE beaty_salon.services
(
   service_id SERIAL PRIMARY KEY NOT NULL,
    service_name varchar(100) NOT NULL,
	description varchar(255),
	category_id serial references beaty_salon.service_category(category_id),
	duration int4 NOT NULL,
	price numeric NOT NULL,
	notes text,
	created_at timestamp NOT NULL,
	updated_at timestamp NOT NULL
);
 ```
 **Таблица Статусы посещений**
```
CREATE TABLE beaty_salon.visit_status
(
   status_id SERIAL PRIMARY KEY NOT NULL,
    status_name varchar(50) NOT NULL,
	notes text,
	created_at timestamp NOT NULL,
	updated_at timestamp NOT NULL
);
 ```
 **Таблица Посещения**
```
CREATE TABLE beaty_salon.visit
(
   visit_id SERIAL PRIMARY KEY NOT NULL,
    client_id serial references beaty_salon.clients(client_id),
	employee_id serial references beaty_salon.employee(employee_id),
    visit_date date,
	service_id serial references beaty_salon.services(service_id),
	status_id serial references beaty_salon.visit_status(status_id),
	created_at timestamp NOT NULL,
	updated_at timestamp NOT NULL
);
 ```
 > Созданные таблицы
>>![Результат 8](/DataBase/tables.png)

 ## Создание таблиц БД в другой схеме (beaty)
 **Таблица Продукция салона**
```
CREATE TABLE beaty.products
(
    id SERIAL PRIMARY KEY NOT NULL,
    product_name varchar(100) ,
	notes text,
	price numeric NOT NULL,
	created_at timestamp NOT NULL,
	updated_at timestamp NOT NULL
);
 ```
 **Таблица Покупки клиентов**
```
CREATE TABLE beaty.purchase
(
    id SERIAL PRIMARY KEY NOT NULL,
    product_id SERIAL references beaty.products(id),
	client_id serial references beaty_salon.clients(client_id),
	notes text,
	amount numeric NOT NULL,
	created_at timestamp NOT NULL,
	updated_at timestamp NOT NULL
);
 ```