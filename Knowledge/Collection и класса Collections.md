---
tags:
  - Java
---
Вот сравнение интерфейса `Collection` и класса `Collections` в Java, включая методы и описание, с добавлением столбца с эмодзи для удобного восприятия.

### Сравнение: Collection и Collections

|     | **Свойство**        | **Collection**                                                                                      | **Collections**                                                                                                     |
| --- | ------------------- | --------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| 📚  | **Тип**             | Интерфейс, служит основой для всех коллекций                                                        | Утилитарный класс, предоставляющий статические методы для работы с коллекциями                                      |
| 🔗  | **Иерархия**        | Является родительским интерфейсом для различных коллекций (`List`, `Set`, `Queue`)                  | Не относится напрямую к иерархии коллекций, но содержит методы для работы с любыми `Collection` объектами           |
| ⚙️  | **Основные методы** | `add()`, `remove()`, `size()`, `isEmpty()`, `contains()`, и другие методы для управления коллекцией | `sort()`, `shuffle()`, `reverse()`, `min()`, `max()`, `singletonList()`, и другие утилиты для работы с коллекциями  |
| 🔄  | **Использование**   | Определяет основные операции для всех коллекций                                                     | Используется для выполнения операций над коллекциями, таких как сортировка, преобразование и другие общие алгоритмы |

### Основные методы интерфейса Collection

| **Метод**                                     | **Описание**                                                                                     | **Эмодзи**  |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------|-------------|
| `boolean add(E e)`                            | Добавляет указанный элемент в коллекцию.                                                       | ➕          |
| `boolean remove(Object o)`                    | Удаляет указанный элемент из коллекции, если он присутствует.                                  | ➖          |
| `boolean contains(Object o)`                  | Проверяет, содержится ли указанный элемент в коллекции.                                        | 🔍          |
| `int size()`                                  | Возвращает количество элементов в коллекции.                                                   | 📏          |
| `boolean isEmpty()`                           | Проверяет, пуста ли коллекция.                                                                  | 🗑️          |
| `Iterator<E> iterator()`                      | Возвращает итератор для перебора элементов в коллекции.                                        | 🔄          |

### Основные методы класса Collections

| **Метод**                                    | **Описание**                                                                                     | **Эмодзи**  |
|----------------------------------------------|--------------------------------------------------------------------------------------------------|-------------|
| `static <T> void sort(List<T> list)`        | Сортирует указанный список в естественном порядке.                                             | 📊          |
| `static <T> void shuffle(List<T> list)`     | Перемешивает элементы указанного списка в случайном порядке.                                   | 🔀          |
| `static <T> T min(Collection<? extends T> coll)` | Возвращает минимальный элемент из коллекции.                                          | ⬇️         |
| `static <T> T max(Collection<? extends T> coll)` | Возвращает максимальный элемент из коллекции.                                          | ⬆️         |
| `static <T> List<T> singletonList(T o)`     | Возвращает неизменяемый список, содержащий только указанный элемент.                          | 🏷️          |
| `static void reverse(List<?> list)`          | Обращает порядок элементов в указанном списке.                                                | 🔄          |

### Примеры использования

#### Пример использования Collection

```java
import java.util.ArrayList;
import java.util.Collection;

public class CollectionExample {
    public static void main(String[] args) {
        Collection<String> collection = new ArrayList<>();

        // Добавление элементов
        collection.add("A");
        collection.add("B");
        collection.add("C");

        // Проверка размера
        System.out.println("Size: " + collection.size()); // Вывод: Size: 3

        // Проверка на наличие элемента
        System.out.println("Contains 'A': " + collection.contains("A")); // Вывод: true

        // Удаление элемента
        collection.remove("B");

        // Итерация по элементам
        for (String item : collection) {
            System.out.println("Item: " + item);
        }

        // Очистка коллекции
        collection.clear();
        System.out.println("Is empty: " + collection.isEmpty()); // Вывод: true
    }
}
```

#### Пример использования Collections

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class CollectionsExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("B");
        list.add("A");
        list.add("C");

        // Сортировка списка
        Collections.sort(list);
        System.out.println("Sorted List: " + list); // Вывод: Sorted List: [A, B, C]

        // Перемешивание списка
        Collections.shuffle(list);
        System.out.println("Shuffled List: " + list);

        // Мин/макс
        String minElement = Collections.min(list);
        String maxElement = Collections.max(list);
        System.out.println("Min: " + minElement + ", Max: " + maxElement);
    }
}
```

Эти таблицы и примеры предоставляют ясное представление о различиях между интерфейсом `Collection` и классом `Collections` в Java, а также их соответствующих методах.