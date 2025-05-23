---
tags:
  - Java
---

> [!NOTE]
> **HashMap** — это класс, который представляет собой коллекцию, использующую хеш-таблицу для хранения данных, где каждое значение сопоставляется с уникальным ключом. Это одна из наиболее часто используемых реализаций интерфейса `Map`, обеспечивающая высокую производительность для операций добавления, удаления и поиска элементов. (Легко представить реализацию как один связный список поделенный на несколько для скорости работы, тк мы будем знать в каком конкретно лежит наш key)

[[Основной процесс добавления в HashMap]]
[[Использование сбалансированных деревьев в HashMap]]

![[Pasted image 20250326135609.png]]

![[Pasted image 20250326134246.png]]

## Основные характеристики HashMap

1. **Структура данных**: Использует хеширование для организации данных, что позволяет осуществлять операции со сложностью O(1) в среднем случае.
2. **Не гарантирует порядок**: Порядок элементов не гарантируется. Если нужен порядок, следует использовать `LinkedHashMap`.
3. **Null ключи и значения**: Позволяет хранить один `null` ключ и любое количество `null` значений.
4. **Не синхронизирован**: Это означает, что для обеспечения потокобезопасности необходимо использовать внешнюю синхронизацию.

## Основные методы класса HashMap

|     | Метод                                    | Описание                                                  |
| --- | ---------------------------------------- | --------------------------------------------------------- |
| ➕   | `put(K key, V value)`                    | Добавляет пару ключ-значение в карту.                     |
| 🔍  | `get(Object key)`                        | Возвращает значение, сопоставленное с указанным ключом.   |
| ❌   | `remove(Object key)`                     | Удаляет элемент по указанному ключу.                      |
| ✔️  | `containsKey(Object key)`                | Проверяет наличие указанного ключа.                       |
| 📏  | `size()`                                 | Возвращает количество элементов в карте.                  |
| 🗑️ | `clear()`                                | Удаляет все пары ключ-значение из карты.                  |
| 🗝️ | `keySet()`                               | Возвращает набор всех ключей в карте.                     |
| 📚  | `values()`                               | Возвращает коллекцию всех значений в карте.               |
| 🔗  | `entrySet()`                             | Возвращает набор всех пар ключ-значение в карте.          |
| 🧐  | `containsValue(Object value)`            | Проверяет наличие указанного значения в карте.            |
| ➕📦 | `putAll(Map<? extends K,? extends V> m)` | Добавляет все пары ключ-значение из другой карты.         |
| 🔄  | `replace(K key, V value)`                | Заменяет значение, сопоставленное с указанным ключом.     |
| 🔀  | `replace(K key, V oldValue, V newValue)` | Заменяет значение только при совпадении старого значения. |

Эта таблица включает больше методов класса `HashMap`, что позволяет лучше понять его возможности и функциональность.

![[Pasted image 20250326134302.png]]
## 1. Начальная емкость (Initial Capacity)

- **Определение**: Начальная емкость – это первоначальный размер массива, который используется для хранения элементов в структуре данных, такой как хеш-таблица.
- **Значение**: Установка начальной емкости позволяет оптимизировать производительность, поскольку она может уменьшить количество перераспределений памяти, если вы заранее знаете, сколько элементов будете хранить.
  
  Пример: 
  - Если вы знаете, что будет добавлено около 100 элементов, вы можете установить начальную емкость на 100. Это может быть более эффективным, чем использование дефолтной начальной емкости (часто 16 в Java), которая приведет к частым увеличениям емкости.

## 2. Коэффициент загрузки (Load Factor)

- **Определение**: Коэффициент загрузки – это значение, определяющее, насколько заполненной должна быть хеш-таблица, прежде чем произойдет увеличение емкости.
- **Значение**: Этот коэффициент в основном указывает, какую долю емкости вы можете использовать, прежде чем таблицу нужно будет увеличить. Обычно его значение колеблется от 0.5 до 0.75:
  - Например, когда коэффициент загрузки равен 0.75, это означает, что когда заполненность таблицы достигает 75% от ее текущей емкости, хеш-таблица будет автоматически увеличена.
  
  Пример:
  - Если начальная емкость хеш-таблицы составляет 16 и коэффициент загрузки составляет 0.75, то при добавлении около 12 элементов (75% от 16) таблица будет увеличена, чтобы обеспечить больше места для новых элементов.


### Пример кода

```java
import java.util.HashMap;
import java.util.Map;

public class HashMapDemo {
    public static void main(String[] args) {
        // Создание экземпляра HashMap
        HashMap<String, Integer> map = new HashMap<>();

        // 1. Добавление элементов в HashMap (put)
        map.put("Alice", 25);
        map.put("Bob", 30);
        map.put("Charlie", 35);
        
        // 2. Получение элементов (get)
        System.out.println("Возраст Alice: " + map.get("Alice")); // Возраст Alice: 25

        // 3. Обновление значения (put)
        map.put("Alice", 26);
        System.out.println("Обновленный возраст Alice: " + map.get("Alice")); // Обновленный возраст Alice: 26

        // 4. Проверка наличия ключа (containsKey)
        if (map.containsKey("Bob")) {
            System.out.println("Возраст Bob: " + map.get("Bob")); // Возраст Bob: 30
        }

        // 5. Удаление элемента (remove)
        map.remove("Charlie");
        System.out.println("После удаления Charlie: " + map);

        // 6. Перебор пар ключ-значение (entrySet)
        System.out.println("Все элементы в HashMap:");
        for (Map.Entry<String, Integer> entry : map.entrySet()) {
            System.out.println("Ключ: " + entry.getKey() + ", Значение: " + entry.getValue());
        }

        // 7. Получение размера HashMap (size)
        System.out.println("Размер HashMap: " + map.size()); // Размер HashMap: 2

        // 8. Очистка HashMap (clear)
        map.clear();
        System.out.println("После очистки, размер HashMap: " + map.size()); // Размер HashMap: 0
    }
}
```

### Объяснение кода

1. **Создание HashMap**: Мы создаём экземпляр `HashMap`, где ключи — это строки, а значения — целые числа.
  
2. **Добавление элементов**: Используем метод `put(key, value)` для добавления пар ключ-значение.
  
3. **Получение значений**: Метод `get(key)` используется для получения значения по заданному ключу.
  
4. **Обновление значений**: Чтобы обновить значение, мы просто вызываем метод `put(key, newValue)` с тем же ключом.

5. **Проверка наличия ключа**: Метод `containsKey(key)` позволяет проверить, существует ли заданный ключ в `HashMap`.

6. **Удаление элемента**: Мы используем метод `remove(key)` для удаления пары ключ-значение по ключу.

7. **Перебор элементов**: Метод `entrySet()` возвращает множество пар ключ-значение, позволяя перебрать все элементы с помощью цикла.

8. **Получение размера**: Метод `size()` возвращает текущее количество элементов в `HashMap`.

9. **Очистка HashMap**: Метод `clear()` удаляет все пары ключ-значение из карты.

> [!tip]
> ## Когда использовать HashMap
> 
> `HashMap` полезен в следующих случаях:
> 
> - **Хранение пар ключ-значение**: Когда необходимо быстро находить значения по уникальным ключам.
> - **Необходимость работы с динамическими данными**: Если количество элементов неизвестно заранее и может изменяться во время выполнения программы.
> - **Отсутствие требований к порядку хранения**: Когда порядок элементов не имеет значения.
> 

## Заключение

Класс `HashMap` предоставляет мощное и эффективное средство для работы с коллекциями пар ключ-значение. Благодаря своей высокой производительности и простоте использования `HashMap` является одним из наиболее популярных классов в Java для работы с неупорядоченными данными. Тем не менее, стоит помнить о его особенностях, таких как отсутствие гарантии порядка и необходимость внешней синхронизации для потокобезопасности.