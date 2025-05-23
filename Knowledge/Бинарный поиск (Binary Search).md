---
tags:
  - Алгоритмы
---
**Бинарный поиск** — это эффективный алгоритм поиска элемента в **отсортированном** массиве, который имеет временную сложность $O(\log n)$. Он работает с помощью деления массива пополам и последующего выбора половины, в которой потенциально может находиться искомый элемент.

## Основная идея бинарного поиска

1. **Инициализация**: Установите два указателя: `low`, который указывает на начало массива, и `high`, который указывает на конец массива.
2. **Цикл поиска**: 
   - Вычислите средний индекс массива: `mid = (low + high) / 2`.
   - Сравните элемент с рядом `mid`.
     - Если элемент равен искомому значению, верните индекс `mid`.
     - Если элемент меньше искомого значения, переместите указатель `low` на `mid + 1`.
     - Если элемент больше, переместите указатель `high` на `mid - 1`.
3. **Завершение**: Если значение не найдено, возвращайте -1 или любое другое значение, указывающее на отсутствие элемента в массиве.

## Пример реализации на Java

Вот пример реализации бинарного поиска на языке Java:

```java
public class BinarySearch {
    public static int binarySearch(int[] array, int target) {
        int low = 0;
        int high = array.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2; // Вычисление среднего индекса

            if (array[mid] == target) {
                return mid; // Возвращаем индекс, если элемент найден
            }

            if (array[mid] < target) {
                low = mid + 1; // Ищем в правой половине
            } else {
                high = mid - 1; // Ищем в левой половине
            }
        }

        return -1; // Элемент не найден
    }

    public static void main(String[] args) {
        int[] sortedArray = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
        int target = 7;
        int result = binarySearch(sortedArray, target);

        if (result != -1) {
            System.out.println("Элемент найден на индексе: " + result);
        } else {
            System.out.println("Элемент не найден.");
        }
    }
}
```

## Вывод программы

При выполнении кода выше, программа вернет следующий вывод:

```
Элемент найден на индексе: 6
```

## Преимущества и недостатки

### Преимущества
- **Быстрота**: Бинарный поиск значительно быстрее линейного поиска, особенно для больших массивов, благодаря логарифмической сложности.
- **Эффективность**: Не требует дополнительных ресурсов на хранение элементов.

### Недостатки
- **Предварительная сортировка**: Массив должен быть отсортирован перед использованием бинарного поиска.
- **Не подходит для всех структур данных**: Работает только с массивами или коллекциями, поддерживающими произвольный доступ к элементам.

## Заключение

Бинарный поиск — это мощный алгоритм, который обеспечивает эффективный поиск в отсортированных данных. Его простота и быстрота делают его популярным выбором для решения задач, связанных с поиском.