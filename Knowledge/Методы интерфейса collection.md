---
tags:
  - Java
---

### Методы интерфейса Collection

|      | **Метод**                                   | **Описание**                                                                                      |
| ---- | ------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| ➕    | `boolean add(E e)`                          | Добавляет указанный элемент в коллекцию.                                                          |
| ➖    | `boolean remove(Object o)`                  | Удаляет указанный элемент из коллекции, если он присутствует.                                     |
| 🔍   | `boolean contains(Object o)`                | Проверяет, содержится ли указанный элемент в коллекции.                                           |
| 📏   | `int size()`                                | Возвращает количество элементов в коллекции.                                                      |
| 🗑️  | `boolean isEmpty()`                         | Проверяет, пуста ли коллекция.                                                                    |
| 🔄   | `Iterator<E> iterator()` [[Iterator]]       | Возвращает итератор для перебора элементов в коллекции.                                           |
| 📦   | `Object[] toArray()`                        | Возвращает массив, содержащий все элементы коллекции.                                             |
| 📥   | `<T> T[] toArray(T[] a)`                    | Возвращает массив, содержащий все элементы коллекции, и сохраняет в него элементы заданного типа. |
| 📊   | `boolean containsAll(Collection<?> c)`      | Проверяет, содержит ли коллекция все элементы из указанной коллекции.                             |
| ➕📦  | `boolean addAll(Collection<? extends E> c)` | Добавляет все элементы из указанной коллекции в текущую коллекцию.                                |
| ➖📦  | `boolean removeAll(Collection<?> c)`        | Удаляет из коллекции все элементы, содержащиеся в указанной коллекции.                            |
| 🔄📉 | `boolean retainAll(Collection<?> c)`        | Удаляет из коллекции все элементы, не содержащиеся в указанной коллекции.                         |
| 🧹   | `void clear()`                              | Удаляет все элементы из коллекции.                                                                |
| ⚖️   | `boolean equals(Object o)`                  | Сравнивает текущую коллекцию с указанным объектом.                                                |
| 💻   | `int hashCode()`                            | Возвращает хэш-код для текущей коллекции.                                                         |

### Пример использования

Ниже приведен простой пример использования некоторых методов интерфейса `Collection` с `ArrayList`:

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

Эта таблица теперь содержит эмодзи для более простого восприятия методов интерфейса `Collection` и их функциональности.