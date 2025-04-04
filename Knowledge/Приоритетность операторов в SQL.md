---
tags:
  - SQL
---



## Общие правила приоритета операторов

### 1. **Классификация операторов**

Операторы в SQL можно классифицировать по группам, каждая из которых имеет свой уровень приоритета:

#### Высокий приоритет

- **Арифметические операторы**: `*`, `/`, `%` (умножение, деление, остаток от деления)
- **Унарные операторы**: `+`, `-` (положительное и отрицательное значения)

#### Средний приоритет

- **Сравнительные операторы**: `=`, `<>`, `<`, `>`, `<=`, `>=` (равенство и сравнение)
- **`BETWEEN`, `LIKE`, `IN`**: Для диапазонов и подстановок

#### Низкий приоритет

- **Логические операторы**: `AND`, `OR`, `NOT`
- **`IS NULL`, `IS NOT NULL`**: Для проверки на `NULL`

### 2. **Приоритет операторов**

Вот сводная таблица приоритета операторов в SQL от высшего к низшему:
![[Pasted image 20250312230710.png]]


### 3. **Примеры использования приоритета операторов**

#### Пример 1: Смешанные операции

Когда в запросе используются несколько разных операторов, важно помнить о приоритете. Рассмотрим следующий пример:

```sql
SELECT 10 + 5 * 2;  -- Первым выполняется умножение: 10 + 10 = 20
```

#### Пример 2: Использование скобок

Скобки могут быть использованы для явного задания порядка выполнения операций. Они имеют самый высокий приоритет:

```sql
SELECT (10 + 5) * 2;  -- Сначала выполняется сложение: 15 * 2 = 30
```

### 4. **Логические операторы**

При использовании нескольких логических операторов порядок их обработки также определен. Например:

```sql
SELECT * FROM table 
WHERE a > 5 OR b < 10 AND c = 'yes';
```

В этом запросе сначала выполняется `AND`, а затем `OR`. Для явной расстановки приоритета лучше использовать скобки:

```sql
SELECT * FROM table 
WHERE a > 5 OR (b < 10 AND c = 'yes');
```

