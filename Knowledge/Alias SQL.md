---
tags:
  - SQL
---
В SQL, использование псевдонимов (alias) позволяет давать временные имена столбцам или таблицам, что делает ваш запрос более читаемым и упрощает работу с данными. 

## Псевдонимы для столбцов

Псевдонимы столбцов используются для изменения наименования выводимых данных или для упрощения их понимания. Псевдонимы создаются с использованием ключевого слова `AS`, хотя использование этого ключевого слова не является обязательным.

### Синтаксис

```sql
SELECT column_name AS alias_name
FROM table_name;
```

### Пример

```sql
SELECT first_name AS name, last_name AS surname
FROM employees;
```

## Псевдонимы для таблиц

Псевдонимы таблиц упрощают обращение к таблицам, особенно в запросах с множественными джойнами или подзапросами.

### Синтаксис

```sql
SELECT alias_name.column_name
FROM table_name AS alias_name;
```

### Пример

```sql
SELECT e.first_name, e.last_name
FROM employees AS e
JOIN departments AS d ON e.department_id = d.id;
```

## Комбинируя псевдонимы

Вы можете комбинировать псевдонимы для столбцов и таблиц, чтобы сделать запросы максимально понятными.

### Пример

```sql
SELECT 
    e.first_name AS name,
    e.last_name AS surname,
    d.department_name AS department
FROM 
    employees AS e
JOIN 
    departments AS d ON e.department_id = d.id;
```

## Псевдонимы в агрегатах

Псевдонимы также полезны при использовании агрегатных функций, чтобы указать, что вы имеете в виду определённое значение.

```sql
SELECT 
    department_id,
    COUNT(*) AS employee_count,
    AVG(salary) AS average_salary
FROM 
    employees
GROUP BY 
    department_id;
```

## Заключение

Использование псевдонимов в SQL делает ваши запросы более понятными и удобными для чтения. Это особенно полезно в сложных запросах, которые включают различные таблицы и агрегатные функции.