# DML в Postgres
## Применение регулярных выражений

### Оператор SIMILAR TO
Выберем всех клиентов из таблицы clients, чье имя начинается на И или Л
```
SELECT * FROM beaty_salon.clients
where first_name similar to'[ИЛ]%'
```
**Результат использования**
![Результат](/Potgres/like.png)

### Очистка номеров телефонов от символов
```
SELECT last_name, first_name, phone, regexp_replace(phone, '[^\d]', '', 'g') as phone_clean
FROM beaty_salon.clients
```
**Результат использования**
![Результат](/Potgres/clean.png)

## Применение INNER JOIN

```
select beaty_salon.employee.first_name, beaty_salon.employee.last_name,beaty_salon.employee.middle_name,beaty_salon.employee.hire_date, beaty_salon.specialization.specialization_name from beaty_salon.employee
inner join beaty_salon.specialization
on beaty_salon.employee.specialization_id = beaty_salon.specialization.specialization_id
```
**Результат использования INNER JOIN**
![Результат JOIN](/Potgres/join1.png)

## Применение LEFT JOIN

```
select beaty_salon.employee.first_name, beaty_salon.employee.last_name,beaty_salon.employee.middle_name,beaty_salon.employee.hire_date, beaty_salon.specialization.specialization_name from beaty_salon.employee
left join beaty_salon.specialization
on beaty_salon.employee.specialization_id = beaty_salon.specialization.specialization_id
```
**Результат использования LEFT JOIN**
![Результат JOIN](/Potgres/joinleft.png)

В данном случае левой таблицей считается таблица employee. В результат попадают записи, совпадающие по ключу и все записи из левой таблицы, для которых нет соответствия в правой (правой в данном случае является specialization)

**Результат использования LEFT JOIN с измененным порядком соединения в FROM**
![Результат JOIN](/Potgres/joinleft2.png)

Здесь же левой таблицей считается specialization. Поэтому в результате помимо записей совпадающих по ключу есть записи из таблицы specialization, для которых нет пары в правой (правая здесь specialization)

## Применение Returning

Получим данные из модифицируемых строк в процессе их обработки.
```
insert into beaty_salon.service_category (category_id,category_name,description,created_at,updated_at)
values (303,'Массаж','Различные виды массажа',now(),now())
RETURNING beaty_salon.service_category.category_id;
```
**Результат использования**
![Результат](/Potgres/return.png)

## Применение UPDATE FROM
```
UPDATE beaty_salon.services SET category_id = beaty_salon.service_category.category_id FROM beaty_salon.service_category WHERE beaty_salon.services.category_id = beaty_salon.service_category.category_id
```
**Результат использования**
![Результат](/Potgres/up.png)
![Результат](/Potgres/update.png)

## Применение DELETE с USING
Удалим записи из таблицы services, используя соответствие условиям в другой таблице (service_category)
```
DELETE FROM beaty_salon.services USING beaty_salon.service_category
WHERE beaty_salon.services.category_id = beaty_salon.service_category.category_id;
```
![Результат](/Potgres/delete.png)
