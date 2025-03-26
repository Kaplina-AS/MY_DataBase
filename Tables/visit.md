# **Таблица Посещения** (visit)
## Структура таблицы Посещения 
Таблица Посещения содержит основную информацию о посещениях клиентов салона.
|Название атрибута|Тип данных|Описание атрибута|Ограничения|Обязательность|
|-|-------|---|-|-|
|visit_id|uuid|Уникальный идентификатор записи|PRIMARY KEY|NOT NULL|
|client_id|uuid|Идентификатор клиента|FOREIGN KEY|NOT NULL|
|employee_id|uuid|Идентификатор cотрудника|FOREIGN KEY|NOT NULL|
|visit_date|date|Дата посещения| |NOT NULL|
|service_id|uuid|Идентификатор услуги|FOREIGN KEY|NOT NULL|
|status_id|uuid|Идентификатор статуса услуги|FOREIGN KEY|NOT NULL|
|created_at|timestamp|Дата создания записи| |NOT NULL|
|updated_at|timestamp|Дата обновления записи| |NOT NULL|\
## Создание индексов для таблицы Посещения 
 #### Простой индекс
 ```
 create index idx_visit_date
on visit (visit_date)
 ```
 В базе данных поиск посещений по дате ускорит поиск записей.
#### Составной индекс
 ```
 create index idx_visit_date_status
on visit (visit_date, status_id)
 ```
 Составной индекс может ускорить поиск записей, например, по условию выбора даты и статуса услуги в эту дату.