---
tags:
  - Java
---

> [!NOTE]
> ### Определение
> **Function** в Java — это функциональный интерфейс, который представляет собой операцию, принимающую один аргумент и возвращающую результат. Этот интерфейс принадлежит пакету `java.util.function` и широко используется для преобразования данных.

### Основные Характеристики
- **Принимает один аргумент:** Метод `apply(T t)` принимает один параметр и выполняет операцию.
- **Возвращает результат:** Метод возвращает результат преобразования, который может быть другим типом.

### Пример Использования

Рассмотрим сценарий, где мы хотим преобразовать строку в её длину. Вот как это можно сделать с использованием интерфейса Function:

```java
import java.util.function.Function;

public class FunctionExample {
    public static void main(String[] args) {
        // Создание Function, который определяет длину строки
        Function<String, Integer> stringLength = str -> str.length();

        // Использование Function
        Integer length = stringLength.apply("Привет, мир!");
        System.out.println("Длина строки: " + length); // Вывод: Длина строки: 13
    }
}
```

### Когда Использовать Function
- **Преобразование данных:** Когда вам нужно изменить или преобразовать данные из одного формата в другой. Например, конвертация значений или обработка объектов.
- **В Stream API:** Для обработки коллекций, например, преобразования элементов списка с помощью метода `map()`.

### Методы для Комбинации
Интерфейс Function также предоставляет методы для комбинирования других функций:

- **andThen:** Применяет текущую функцию, а затем другую функцию:
  ```java
  Function<Integer, String> toString = Object::toString;
  Function<String, String> combined = toString.andThen(str -> "Число: " + str);
  
  System.out.println(combined.apply(42)); // Вывод: Число: 42
  ```

- **compose:** Применяет другую функцию, а затем текущую:
  ```java
  Function<Integer, Integer> addOne = x -> x + 1;
  Function<Integer, Integer> multiplyByTwo = x -> x * 2;
  
  Function<Integer, Integer> combined = multiplyByTwo.compose(addOne);
  System.out.println(combined.apply(3)); // Вывод: 8 (первоначально 3 + 1 = 4, затем 4 * 2 = 8)
  ```

### Заключение
Интерфейс Function в Java — это мощный инструмент для преобразования данных, который хорошо подходит для применения в функциональном программировании. Его простота и возможность комбинирования делают его универсальным для множества задач, отражая основные принципы работы с данными в современном Java.