---
tags:
  - Java
---

> [!info]
> ## Коллекции в Java
> 
> **Коллекции** в Java представляют собой структуры данных, которые позволяют хранить и управлять группами объектов. Java предоставляет несколько интерфейсов и классов для работы с коллекциями, которые находятся в пакете `java.util`. Основные типы коллекций включают:

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
  - `LinkedHashSet`: сохраняет порядок добавления элементов.
  - [[TreeSet]]: упорядоченное множество; элементы хранятся в отсортированном виде.

![[Pasted image 20250330153616.png]]

![[Pasted image 20250330160010.png]]

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

### 4. **Стек (Stack)**
Стек представляет собой структуру данных, работающую по принципу "последний пришёл — первый вышел" (LIFO).

> [!tip]
> ### Преимущества использования коллекций:
> 
> - Гибкость в управлении данными.
> - Удобные методы для работы с элементами.
> - Поддержка различных алгоритмов сортировки и поиска.


