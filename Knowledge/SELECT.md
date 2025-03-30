---
tags:
  - SQL
---

> [!NOTE]
> # Команда `SELECT` в SQL
> 
> Команда `SELECT` является одной из самых важных и основных команд в SQL. Она используется для извлечения данных из таблиц баз данных. С помощью `SELECT` можно выполнять выборку конкретных полей, добавлять условия, сортировать и группировать данные.


![[Pasted image 20250311214426.png]]
## Основной синтаксис
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

## Основные компоненты команды `SELECT`

### 1. Выбор столбцов (Projection)
- Для выбора конкретных столбцов указывайте их имена, разделяя запятыми.
- Чтобы выбрать все столбцы из таблицы, используйте символ `*`.

#### Пример
```sql
SELECT first_name, last_name FROM employees;
```
Или для выбора всех столбцов:
```sql
SELECT * FROM employees;
```

### 2. Указание таблицы
- Используйте оператор `FROM`, чтобы указать таблицу, из которой необходимо извлечь данные.

### 3. Условия с оператором `WHERE`
- Условие `WHERE` позволяет фильтровать записи, возвращая только те, что удовлетворяют заданному критерию.

#### Пример
```sql
SELECT * FROM employees WHERE department = 'Sales';
```

### 4. Сортировка данных с помощью `ORDER BY`
- С помощью `ORDER BY` можно сортировать результаты по одному или нескольким полям. По умолчанию сортировка выполняется по возрастанию; для сортировки по убыванию используйте `DESC`.

#### Пример
```sql
SELECT * FROM employees ORDER BY last_name ASC;
```

### 5. Группировка данных с помощью `GROUP BY`
- `GROUP BY` используется для группировки записей с одинаковыми значениями в указанных столбцах, что позволяет выполнять агрегатные функции, такие как `COUNT`, `SUM`, `AVG`.

#### Пример
```sql
SELECT department, COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

### 6. Агрегатные функции
- SQL предоставляет несколько агрегатных функций для анализа данных:
  - `COUNT()` — подсчет количества строк.
  - `SUM()` — сумма значений столбца.
  - `AVG()` — среднее значение столбца.
  - `MIN()` — минимальное значение.
  - `MAX()` — максимальное значение.

#### Пример
```sql
SELECT AVG(salary) AS average_salary FROM employees;
```

### 7. Использование `JOIN` для объединения таблиц
- `JOIN` позволяет объединять данные из разных таблиц, основываясь на связанных столбцах.

#### Пример
```sql
SELECT e.first_name, e.last_name, d.department_name
FROM employees e
JOIN departments d ON e.department_id = d.id;
```

### 8. Примеры использования подзапросов
- Подзапросы позволяют включать результаты одного запроса в другой.

#### Пример
```sql
SELECT * FROM employees
WHERE department_id IN (SELECT id FROM departments WHERE location = 'New York');
```



> [!NOTE]
> В SQL, использование выражений в списке SELECT позволяет вам извлекать и обрабатывать данные, преобразуя их по мере необходимости перед отображением. Ниже приведены основные моменты о том, как использовать выражения в списке SELECT.

## Основные Принципы Работы

### 1. **Арифметические выражения**
Вы можете выполнять арифметические операции с полями таблицы. Пример:

```sql
SELECT 
    price, 
    quantity, 
    price * quantity AS total_cost
FROM 
    products;
```

### 2. **Функции агрегирования**
Функции, такие как `SUM()`, `AVG()`, и `COUNT()`, могут быть использованы для вычисления значений на основе группы данных.

```sql
SELECT 
    category, 
    COUNT(*) AS product_count, 
    AVG(price) AS average_price
FROM 
    products
GROUP BY 
    category;
```

### 3. **Строковые функции**
Выражения позволяют работать со строками. Например, вы можете объединять строки с помощью `CONCAT()` или использовать `UPPER()` для преобразования регистра:

```sql
SELECT 
    CONCAT(first_name, ' ', last_name) AS full_name,
    UPPER(email) AS email_upper
FROM 
    users;
```

### 4. **Условия (CASE)**
Вы можете использовать конструкцию `CASE` для условий в вашем запросе.

```sql
SELECT 
    order_id,
    CASE 
        WHEN status = 'shipped' THEN 'Order has been shipped'
        WHEN status = 'pending' THEN 'Order is pending'
        ELSE 'Unknown status'
    END AS order_status
FROM 
    orders;
```

### 5. **Логические выражения**
Выражения также могут включать логические операторы, такие как `AND`, `OR`, `NOT`:

```sql
SELECT 
    product_name, 
    price,
    CASE 
        WHEN price > 100 THEN 'Expensive'
        ELSE 'Affordable'
    END AS price_category
FROM 
    products
WHERE 
    stock > 0 
    AND is_active = 1;
```

## Пример Запроса

Вот полный пример запроса, который учитывает все вышеперечисленные аспекты:

```sql
SELECT 
    p.product_name,
    p.price,
    p.stock,
    CASE 
        WHEN p.price > 100 THEN 'Expensive'
        ELSE 'Affordable'
    END AS price_category,
    SUM(o.quantity) AS total_sales
FROM 
    products p
LEFT JOIN 
    orders o ON p.id = o.product_id
GROUP BY 
    p.product_name, p.price, p.stock
HAVING 
    total_sales > 10
ORDER BY 
    p.price DESC;
```

## Заключение
Использование выражений в списке SELECT в SQL позволяет создавать более сложные запросы и получать данные в нужном формате. Это дает возможность делать анализ данных еще более мощным и гибким.
## Заключение
Команда `SELECT` является мощным инструментом для извлечения и анализа данных в SQL. Понимание различных элементов и возможностей этой команды позволяет создавать гибкие и эффективные запросы, что критично для работы с реляционными базами данных.