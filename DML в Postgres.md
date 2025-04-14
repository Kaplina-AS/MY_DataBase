# DML в Postgres
## Применение INNER JOIN

```
select beaty_salon.employee.first_name, beaty_salon.employee.last_name,beaty_salon.employee.middle_name,beaty_salon.employee.hire_date, beaty_salon.specialization.specialization_name from beaty_salon.employee
inner join beaty_salon.specialization
on beaty_salon.employee.specialization_id = beaty_salon.specialization.specialization_id
```
**Результат использования INNER JOIN**
[Результат JOIN](/Potgres/join1.png)

## Применение LEFT JOIN

```
select beaty_salon.employee.first_name, beaty_salon.employee.last_name,beaty_salon.employee.middle_name,beaty_salon.employee.hire_date, beaty_salon.specialization.specialization_name from beaty_salon.employee
left join beaty_salon.specialization
on beaty_salon.employee.specialization_id = beaty_salon.specialization.specialization_id

```
**Результат использования LEFT JOIN**
[Результат JOIN](/Potgres/joinleft.png)

В данном случае левой таблицей считается таблица employee. В результат попадают записи, совпадающие по ключу и все записи из левой таблицы, для которых нет соответствия в правой (правой в данном случае является specialization)

**Результат использования LEFT JOIN с измененным порядком соединения в FROM**
[Результат JOIN](/Potgres/joinleft2.png)

Здесь же левой таблицей считается specialization. Поэтому в результате помимо записей совпадающих по ключу есть записи из таблицы specialization, для которых нет пары в правой (правая здесь specialization)

