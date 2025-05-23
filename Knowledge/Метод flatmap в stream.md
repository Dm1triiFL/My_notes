---
tags:
  - Java
---

---

# `flatMap`

## Назначение
Метод `flatMap` применяется для "расплющивания" вложенных потоков, то есть преобразования потока элементов, каждый из которых может представлять собой поток или коллекцию, в один плоский поток.

---

## Что делает

- Преобразует каждый элемент исходного потока с помощью функции-лямбда или метода, возвращающей поток (`Stream`).
- Объединяет все полученные потоки в один "плоский" поток, исключая вложенности.

---

## Синтаксис
```java
<R> Stream<R> flatMap(Function<? super T, ? extends Stream<? extends R>> mapper)
```

- `Function<? super T, ? extends Stream<? extends R>> mapper`
  - Функция, которая на входе принимает один элемент из исходного потока и возвращает поток (`Stream`) возможных элементов.

---

## Пример использования
Допустим, есть список слов (строк), и вам нужно получить поток всех символов из всех слов:

```java
List<String> words = Arrays.asList("каша", "суп", "борщ");

List<Character> characters = words.stream()
    .flatMap(word -> word.chars().mapToObj(c -> (char) c))
    .collect(Collectors.toList());
```

Объяснение:
- `word.chars()` — возвращает IntStream символов слова.
- `mapToObj(c -> (char) c)` — преобразует `int` в `Character`.
- `flatMap` объединяет полученные потоки символов из всех слов в один поток.

---

## Для чего используют
- Когда есть коллекции внутри коллекций, и нужно "расплющить" их в один поток.
- Для преобразования данных, где каждый элемент может привести к нескольким значениям.
- Для более читаемых цепочек преобразований без вложенных циклов.

---
