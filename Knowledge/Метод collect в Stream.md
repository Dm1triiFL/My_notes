---
tags:
  - Java
---

---

# Метод `collect` в Java Stream API

## Общая идея
Метод `collect` используется для "сбора" элементов потока в некоторую коллекцию или другую структуру данных.  
При этом он принимает **Collector** — специальный объект, который определяет, как именно происходит сбор данных.

---

# `groupingBy`

## Что делает?
Группирует элементы потока по ключам, формируя `Map<K, List<T>>`, где ключи — значения, полученные по заданному классификатору.

### Синтаксис
```java
Map<K, List<T>> groupedMap = stream.collect(Collectors.groupingBy(classifier));
```

### Пример

```java
List<String> names = Arrays.asList("Anna", "Alex", "Maria", "Mikhail", "Ivan", "Maria");

Map<Character, List<String>> groupedByFirstLetter = names.stream()
    .collect(Collectors.groupingBy(name -> name.charAt(0)));

```
Результат:
```java
{
  'A'=[Anna, Alex],
  'M'=[Maria, Maria],
  'I'=[Ivan],
  'M'=[Mikhail]
}
```

---

## Расширенные возможности
- Можно задавать **дополнительные** коллекторы для агрегации внутри групп (например, подсчет, множество и т.д.).
- Например:

```java
Map<String, Long> countByName = names.stream()
    .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
```

---

# `partitioningBy`

## Что делает?
Делит элементы потока на две части по предикату, возвращая `Map<Boolean, List<T>>`.

### Синтаксис
```java
Map<Boolean, List<T>> partitionedMap = stream.collect(Collectors.partitioningBy(predicate));
```

### Пример

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

Map<Boolean, List<Integer>> evenOdd = numbers.stream()
    .collect(Collectors.partitioningBy(n -> n % 2 == 0));
```

Результат:
```java
{
  false=[1, 3, 5],
  true=[2, 4, 6]
}
```

---

## Отличия между `groupingBy` и `partitioningBy`
| Характеристика | `groupingBy` | `partitioningBy` |
|----------------|--------------|------------------|
| Делит по | произвольному ключу | по булевому условию (да/нет) |
| Возвращает | `Map<K, List<T>>` | `Map<Boolean, List<T>>` |
| Используется для | множественной группировки | бинарного деления |

---

Если хотите — могу подготовить более сложные примеры или показать, как использовать эти коллекторы вместе с другими!