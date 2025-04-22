---
tags:
  - Java
---

> [!info]
> ## Коллекции в Java
> 
> **Коллекции** в Java представляют собой структуры данных, которые позволяют хранить и управлять группами объектов. Java предоставляет несколько интерфейсов и классов для работы с коллекциями, которые находятся в пакете `java.util`. Основные типы коллекций включают:
> 
> ### Преимущества использования коллекций:
> 
> - Гибкость в управлении данными.
> - Удобные методы для работы с элементами.
> - Поддержка различных алгоритмов сортировки и поиска.


[[Методы интерфейса collection]]
[[Collection и класса Collections]]

![[Pasted image 20250321112643.png]]
![[Pasted image 20250330153834.png]]

### 1. **Списки (List)**
Списки представляют собой упорядоченные коллекции, которые могут содержать дубликаты.
- **Основные реализации:**
  - [[ArrayList]]: динамический массив, обеспечивает быстрый доступ по индексу.
  - [[LinkedList]]: двусвязный список, оптимален для операций добавления и удаления.
  - [[Stack]] (но предпочтительнее использовать `Deque` с `ArrayDeque`).
  - [[Vector]]
  
![[Pasted image 20250321112459.png]]

| Эмоджи | Метод                            | Описание                                                                           |
| ------ | -------------------------------- | ---------------------------------------------------------------------------------- |
| ➕      | `boolean add(E e)`               | Добавляет элемент `e` в конец списка.                                              |
| ➕      | `void add(int index, E element)` | Вставляет элемент `element` в указанную позицию `index`.                           |
| 🔄     | `E remove(int index)`            | Удаляет элемент по индексу `index` и возвращает его.                               |
| 🔄     | `boolean remove(Object o)`       | Удаляет первое вхождение элемента `o` из списка.                                   |
| 🔍     | `E get(int index)`               | Возвращает элемент по индексу `index`.                                             |
| 🔍     | `E set(int index, E element)`    | Заменяет элемент по индексу `index` на `element`.                                  |
| 📏     | `int size()`                     | Возвращает количество элементов в списке.                                          |
| 🚫     | `boolean isEmpty()`              | Проверяет, пуст ли список.                                                         |
| 🔍     | `boolean contains(Object o)`     | Проверяет, содержится ли элемент `o` в списке.                                     |
| 🔄     | `int indexOf(Object o)`          | Возвращает индекс первого вхождения элемента `o` или -1, если элемент отсутствует. |
| 🔄     | `ListIterator<E> listIterator()` | Возвращает итератор для перебора элементов списка.                                 |

|     | **Свойство**           | **ArrayList**                                                   | **LinkedList**                                       | **Vector**                              |
| --- | ---------------------- | --------------------------------------------------------------- | ---------------------------------------------------- | --------------------------------------- |
| 📏  | **Структура**          | Массив                                                          | Связный список                                       | Массив                                  |
| 📂  | **Порядок элементов**  | Гарантирован                                                    | Гарантирован                                         | Гарантирован                            |
| ⚡   | **Время добавления**   | O(1) (в конце)                                                  | O(1) (в конце)                                       | O(1) (в конце)                          |
| ⚡   | **Время удаления**     | O(n)                                                            | O(1) (если известен узел)                            | O(n)                                    |
| 🔍  | **Время доступа**      | O(1)                                                            | O(n)                                                 | O(1)                                    |
| 🔒  | **Потокобезопасность** | Нет                                                             | Нет                                                  | Да (синхронизирован)                    |
| 📅  | **Использование**      | Когда требуется быстрый доступ и динамическое изменение размера | Когда требуется частое добавление/удаление элементов | Когда требуется потокобезопасный список |


```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Vector;

public class ListExample {
    public static void main(String[] args) {
        // ArrayList
        ArrayList<String> arrayList = new ArrayList<>();
        arrayList.add("A");
        arrayList.add("B");
        arrayList.add("C");
        System.out.println("ArrayList: " + arrayList); // Порядок гарантирован

        // LinkedList
        LinkedList<String> linkedList = new LinkedList<>();
        linkedList.add("A");
        linkedList.add("B");
        linkedList.add("C");
        System.out.println("LinkedList: " + linkedList); // Порядок гарантирован

        // Vector
        Vector<String> vector = new Vector<>();
        vector.add("A");
        vector.add("B");
        vector.add("C");
        System.out.println("Vector: " + vector); // Порядок гарантирован
    }
}
```


### 2. **Множества (Set)**
Множества представляют собой коллекции, которые не допускают дубликатов.
- **Основные реализации:**
  - [[HashSet]]: основано на хэш-таблице; быстрая работа с элементами, не гарантирует порядок.
  - [[LinkedHashSet]]: сохраняет порядок добавления элементов.
  - [[TreeSet]]: упорядоченное множество; элементы хранятся в отсортированном виде.

![[Pasted image 20250330153616.png]]

|     |                              |                                                                                                                                |
| --- | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| ➕   | `boolean add(E e)`           | Добавляет элемент `e` в множество. Возвращает `true`, если элемент был добавлен; `false`, если множество уже содержит элемент. |
| 🔄  | `boolean remove(Object o)`   | Удаляет элемент `o` из множества. Возвращает `true`, если элемент был удален, `false` - если такая операция была невозможна.   |
| 🔄  | `void clear()`               | Удаляет все элементы из множества.                                                                                             |
| 🔍  | `boolean contains(Object o)` | Проверяет, содержится ли элемент `o` в множестве.                                                                              |
| 📏  | `int size()`                 | Возвращает количество элементов в множестве.                                                                                   |
| 🚫  | `boolean isEmpty()`          | Проверяет, пусто ли множество.                                                                                                 |
| 🔄  | `Iterator<E> iterator()`     | Возвращает итератор, который позволяет перебрать элементы множества.                                                           |
| 🔄  | `Object[] toArray()`         | Возвращает массив, содержащий все элементы множества.                                                                          |
| 📦  | `<T> T[] toArray(T[] a)`     | Возвращает массив, содержащий элементы множества, указанных в массиве `a` с тем же типом.                                      |

|     | **Свойство**             | **HashSet**            | **LinkedHashSet**            | **TreeSet**                         |
| --- | ------------------------ | ---------------------- | ---------------------------- | ----------------------------------- |
| 🗂️ | **Структура**            | Хеш-таблица            | Хеш-таблица + связный список | Красно-черное дерево                |
| 📊  | **Порядок элементов**    | Не гарантирован        | Порядок вставки              | Отсортированный порядок             |
| ⚡   | **Время добавления**     | O(1)                   | O(1)                         | O(log n)                            |
| ⚡   | **Время удаления**       | O(1)                   | O(1)                         | O(log n)                            |
| 🔍  | **Время поиска**         | O(1)                   | O(1)                         | O(log n)                            |
| 🚫  | **Допустимые дубликаты** | Нет                    | Нет                          | Нет                                 |
| 📅  | **Использование**        | Когда порядок не важен | Когда важен порядок вставки  | Когда важен отсортированный порядок |

```java
import java.util.HashSet;
import java.util.LinkedHashSet;
import java.util.TreeSet;

public class SetExample {
    public static void main(String[] args) {
        // HashSet
        HashSet<String> hashSet = new HashSet<>();
        hashSet.add("A");
        hashSet.add("B");
        hashSet.add("C");
        System.out.println("HashSet: " + hashSet); // Порядок не определен

        // LinkedHashSet
        LinkedHashSet<String> linkedHashSet = new LinkedHashSet<>();
        linkedHashSet.add("A");
        linkedHashSet.add("B");
        linkedHashSet.add("C");
        System.out.println("LinkedHashSet: " + linkedHashSet); // Порядок вставки

        // TreeSet
        TreeSet<String> treeSet = new TreeSet<>();
        treeSet.add("B");
        treeSet.add("A");
        treeSet.add("C");
        System.out.println("TreeSet: " + treeSet); // Отсортированный порядок
    }
}
```

### 3. **Ассоциативные массивы (Map)**
Ассоциативные массивы хранят пары "ключ-значение", каждый ключ должен быть уникальным.
- **Основные реализации:**
  - [[HashMap]]: основано на хэш-таблице, быстрая работа, не гарантирует порядок.
  - [[LinkedHashMap]]: сохраняет порядок добавления.
  - [[TreeMap]]: упорядоченное отображение, элементы хранятся в отсортированном порядке ключей.
  
![[Pasted image 20250326124038.png]]

|     | Метод                             | Описание                                                                                                     |
| --- | --------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| ➕   | `V put(K key, V value)`           | Связывает заданный ключ `key` с заданным значением `value`.                                                  |
| 🔄  | `V remove(Object key)`            | Удаляет связывание для заданного ключа `key`. Возвращает удаленное значение или `null`, если ключ не найден. |
| 🔄  | `void clear()`                    | Удаляет все элементы из отображения.                                                                         |
| 🔍  | `V get(Object key)`               | Возвращает значение, связанное с заданным ключом `key`, или `null`, если ключ не существует.                 |
| 🔍  | `boolean containsKey(Object key)` | Проверяет, содержится ли заданный ключ `key` в отображении.                                                  |
| 📏  | `int size()`                      | Возвращает количество пар "ключ-значение" в отображении.                                                     |
| 🚫  | `boolean isEmpty()`               | Проверяет, пусто ли отображение.                                                                             |
| 🔄  | `Set<K> keySet()`                 | Возвращает множество, содержащие все ключи в отображении.                                                    |
| 🔄  | `Collection<V> values()`          | Возвращает коллекцию, содержащую все значения в отображении.                                                 |
| 🔄  | `Set<Map.Entry<K, V>> entrySet()` | Возвращает набор, содержащий все пары "ключ-значение".                                                       |

|     | **Свойство**            | **HashMap**            | **LinkedHashMap**            | **TreeMap**                         |
| --- | ----------------------- | ---------------------- | ---------------------------- | ----------------------------------- |
| 🗂️ | **Структура**           | Хеш-таблица            | Хеш-таблица + связный список | Красно-черное дерево                |
| 📊  | **Порядок элементов**   | Не гарантирован        | Порядок вставки              | Отсортированный по ключу            |
| ⚡   | **Время добавления**    | O(1)                   | O(1)                         | O(log n)                            |
| ⚡   | **Время удаления**      | O(1)                   | O(1)                         | O(log n)                            |
| 🔍  | **Время поиска**        | O(1)                   | O(1)                         | O(log n)                            |
| 🚫  | **Допустимые ключи**    | Один нулевой ключ      | Один нулевой ключ            | Никаких нулевых ключей              |
| 🚫  | **Допустимые значения** | Любые (включая null)   | Любые (включая null)         | Никаких нулевых значений            |
| 📅  | **Использование**       | Когда порядок не важен | Когда важен порядок вставки  | Когда важен отсортированный порядок |


```java
import java.util.HashMap;
import java.util.LinkedHashMap;
import java.util.TreeMap;

public class MapExample {
    public static void main(String[] args) {
        // HashMap
        HashMap<String, Integer> hashMap = new HashMap<>();
        hashMap.put("A", 1);
        hashMap.put("B", 2);
        hashMap.put("C", 3);
        System.out.println("HashMap: " + hashMap); // Порядок не определен

        // LinkedHashMap
        LinkedHashMap<String, Integer> linkedHashMap = new LinkedHashMap<>();
        linkedHashMap.put("A", 1);
        linkedHashMap.put("B", 2);
        linkedHashMap.put("C", 3);
        System.out.println("LinkedHashMap: " + linkedHashMap); // Порядок вставки

        // TreeMap
        TreeMap<String, Integer> treeMap = new TreeMap<>();
        treeMap.put("B", 2);
        treeMap.put("A", 1);
        treeMap.put("C", 3);
        System.out.println("TreeMap: " + treeMap); // Отсортированный порядок
    }
}
```

### 4. **Очереди (Queue)**

Очереди представляют собой коллекции, которые используются для хранения элементов в порядке их добавления. Они работают по принципу FIFO (First In, First Out), то есть первый добавленный элемент будет первым, который будет удален.

- **Основные реализации:**
  - [[LinkedList в качестве Queue]]: реализует интерфейс `Queue` и позволяет работать как с очередью. Подходит для операций, требующих частого добавления и удаления элементов.
  - [[ArrayDeque]]: более производительный вариант для реализации очередей; не имеет ограничений размера и может использоваться как стек.
  - [[PriorityQueue]]: позволяет хранить элементы в порядке их приоритета, а не порядка добавления.

|     | Метод                        | Описание                                                                                                          |
| --- | ---------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| ➕   | `boolean add(E e)`           | Добавляет элемент `e` в очередь. Если добавление прошло неуспешно, бросает исключение.                            |
| ➕   | `boolean offer(E e)`         | Добавляет элемент `e` в очередь. Возвращает `true`, если добавление прошло успешно; в противном случае — `false`. |
| 🔄  | `E remove()`                 | Удаляет и возвращает первый элемент очереди. Если очередь пуста, бросает исключение.                              |
| 🔄  | `E poll()`                   | Удаляет и возвращает первый элемент очереди или `null`, если очередь пуста.                                       |
| 🔍  | `E element()`                | Возвращает первый элемент очереди без его удаления. Если очередь пуста, бросает исключение.                       |
| 🔍  | `E peek()`                   | Возвращает первый элемент очереди без удаления или `null`, если очередь пуста.                                    |
| 📏  | `int size()`                 | Возвращает количество элементов в очереди.                                                                        |
| 🚫  | `boolean isEmpty()`          | Проверяет, пуста ли очередь.                                                                                      |
| 🔍  | `boolean contains(Object o)` | Проверяет, содержится ли элемент `o` в очереди.                                                                   |
| 🔄  | `Iterator<E> iterator()`     | Возвращает итератор, который позволяет перебрать элементы очереди.                                                |
| 📦  | `Object[] toArray()`         | Возвращает массив, содержащий все элементы очереди.                                                               |
| 📦  | `<T> T[] toArray(T[] a)`     | Возвращает массив, содержащий элементы очереди, указанных в массиве `a` с тем же типом.                           |

![[Pasted image 20250331003348.png]]

|     | **Свойство**             | **LinkedList**       | **ArrayDeque**       | **PriorityQueue**               |
| --- | ------------------------ | -------------------- | -------------------- | ------------------------------- |
| 🗂️ | **Структура**            | Связный список       | Динамический массив  | Контейнер с приоритетом         |
| 📊  | **Порядок элементов**    | Гарантирован (FIFO)  | Гарантирован (FIFO)  | По приоритету                   |
| ⚡   | **Время добавления**     | O(1)                 | O(1)                 | O(log n)                        |
| ⚡   | **Время удаления**       | O(1)                 | O(1)                 | O(log n)                        |
| 🔍  | **Время доступа**        | O(n)                 | O(n)                 | O(n)                            |
| 🚫  | **Допустимые дубликаты** | Да                   | Да                   | Да                              |
| 📅  | **Использование**        | Когда требуется FIFO | Когда требуется FIFO | Когда важен приоритет элементов |

```java
import java.util.LinkedList;
import java.util.ArrayDeque;
import java.util.PriorityQueue;

public class QueueExample {
    public static void main(String[] args) {
        // LinkedList как очередь
        LinkedList<String> linkedListQueue = new LinkedList<>();
        linkedListQueue.add("A");
        linkedListQueue.add("B");
        linkedListQueue.add("C");
        System.out.println("LinkedList Queue: " + linkedListQueue);
        
        // Извлечение из очереди
        String first = linkedListQueue.poll(); // Извлекает A
        System.out.println("Dequeued from LinkedList Queue: " + first);
        System.out.println("LinkedList Queue after dequeue: " + linkedListQueue);

        // ArrayDeque
        ArrayDeque<String> arrayDequeQueue = new ArrayDeque<>();
        arrayDequeQueue.add("A");
        arrayDequeQueue.add("B");
        arrayDequeQueue.add("C");
        System.out.println("ArrayDeque Queue: " + arrayDequeQueue);
        
        // Извлечение из очереди
        String firstDeque = arrayDequeQueue.poll(); // Извлекает A
        System.out.println("Dequeued from ArrayDeque Queue: " + firstDeque);
        System.out.println("ArrayDeque Queue after dequeue: " + arrayDequeQueue);

        // PriorityQueue
        PriorityQueue<Integer> priorityQueue = new PriorityQueue<>();
        priorityQueue.add(3);
        priorityQueue.add(1);
        priorityQueue.add(2);
        System.out.println("PriorityQueue: " + priorityQueue);
        
        // Извлечение элемента с наивысшим приоритетом
        int highestPriority = priorityQueue.poll(); // Извлекает 1
        System.out.println("Dequeued from PriorityQueue: " + highestPriority);
        System.out.println("PriorityQueue after dequeue: " + priorityQueue);
    }
}
```

