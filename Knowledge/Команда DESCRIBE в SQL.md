---
tags:
  - SQL
---

Команда `DESCRIBE` (или сокращенно `DESC`) в SQL используется для получения информации о структуре таблицы в реляционных базах данных. Она позволяет пользователю увидеть описания всех столбцов, их типы данных, ограничения и другую важную информацию.

## Синтаксис
```sql
DESCRIBE имя_таблицы;
```
Или
```sql
DESC имя_таблицы;
```

## Параметры
- **имя_таблицы**: Название таблицы, информацию о которой вы хотите получить.

## Выходные данные
Команда `DESCRIBE` возвращает следующие столбцы:

| Столбец      | Описание                                     |
|--------------|----------------------------------------------|
| `Field`      | Имя столбца                                 |
| `Type`       | Тип данных столбца                          |
| `Null`       | Указание на возможность наличия значений NULL |
| `Key`        | Указывает, является ли столбец ключом (PRIMARY, UNIQUE, и т.д.) |
| `Default`    | Значение по умолчанию для столбца          |
| `Extra`      | Дополнительная информация (например, автоинкремент) |

## Пример использования
### Пример 1: Получение информации о таблице
```sql
DESCRIBE employees;
```
**Вывод:**

| Field         | Type         | Null | Key     | Default | Extra             |
|---------------|--------------|------|---------|---------|-------------------|
| id            | int(11)     | NO   | PRI     | NULL    | auto_increment     |
| name          | varchar(50)  | NO   |         | NULL    |                   |
| position      | varchar(50)  | YES  |         | NULL    |                   |
| salary        | decimal(10,2)| YES  |         | NULL    |                   |

### Пример 2: Узнать структуру таблицы 
```sql
DESC products;
```
**Вывод может выглядеть так:**

| Field         | Type         | Null | Key     | Default | Extra            |
|---------------|--------------|------|---------|---------|------------------|
| product_id    | int(11)     | NO   | PRI     | NULL    | auto_increment    |
| product_name  | varchar(255) | NO   |         | NULL    |                  |
| price         | decimal(10,2)| NO   |         | NULL    |                  |
| stock         | int(11)     | YES  |         | NULL    |                  |

## Заключение
Команда `DESCRIBE` является полезным инструментом для быстрого получения информации о структуре таблиц в базе данных. Она упрощает понимание структуры данных, особенно при работе с большими и сложными базами данных.