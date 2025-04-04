---
tags:
  - SQL
---
# Таблица DUAL в Oracle

## Описание

Таблица `DUAL` является специальной системной таблицей в базе данных Oracle. Она предназначена для выполнения запросов, которые требуют наличия таблицы, но не требуют данных из реальной таблицы. `DUAL` содержит одну строку и один столбец и часто используется в SQL-запросах, где необходимо получать данные, не обращаясь к пользователям.

## Структура таблицы DUAL

Таблица `DUAL` имеет следующую структуру:

- **COLUMN_NAME**: Название единственного столбца.
- **DUMMY**: Тип данных `VARCHAR2(1)` со значением `'X'`.

```sql
SELECT * FROM DUAL;
```

Этот запрос вернет:

| DUMMY |
|-------|
| X     |

## Основные применения

### 1. **Выполнение арифметических и других вычислений**

Таблица `DUAL` часто используется для выполнения операций, возвращающих одно значение:

```sql
SELECT 1 + 1 FROM DUAL;  -- Возвращает 2
```

### 2. **Получение значений из функций**

Вы можете вызывать функции, возвращающие одно значение, с использованием таблицы `DUAL`:

```sql
SELECT SYSDATE FROM DUAL;  -- Возвращает текущее системное время
```

### 3. **Создание временных данных**

Если вам нужно создать временные ряды данных или выполнить тестовые запросы, таблица `DUAL` может быть использована, чтобы не создавать отдельные таблицы:

```sql
SELECT 'Hello, World!' AS greeting FROM DUAL;  -- Возвращает значение 'Hello, World!'
```

### 4. **Использование в хранимых процедурах и триггерах**

`DUAL` также может использоваться в контексте хранимых процедур или триггеров для выполнения операций без необходимости работы с реальными таблицами.

## Замечания

- В других СУБД, таких как MySQL или PostgreSQL, аналогичные функции не обязательно требуют специальной таблицы для выполнения подобных операций.
- В Oracle, начиная с версии 12c, существует возможность выполнения запросов без явного указания `FROM DUAL`, если это не требует больше одной строки.
  
```sql
SELECT 1 + 1;  -- Возможно в Oracle 12c и выше
```

## Заключение

Таблица `DUAL` в Oracle является важным инструментом для выполнения SQL-запросов, которые требуют наличия таблицы, но не требуют фактических данных из нее. Это упрощает выполнение различных операций и делает SQL-запросы более универсальными.