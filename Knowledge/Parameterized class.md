---
tags:
  - Java
---
# Параметризованные классы в Java

Параметризованные классы (или обобщенные классы) в Java позволяют создавать классы, которые работают с разными типами данных, обеспечивая безопасность типов на этапе компиляции. Они являются важной частью концепции дженериков в Java.

## Основные понятия

### 1. Определение

Параметризованный класс — это класс, который принимает один или несколько параметров типа. Эти параметры используются в определении полей, методов и конструкторов класса.

### 2. Синтаксис

#### Объявление параметризованного класса

```java
class GenericClass<T> {
    private T data;

    public GenericClass(T data) {
        this.data = data;
    }

    public T getData() {
        return data;
    }

    public void setData(T data) {
        this.data = data;
    }
}
```

### 3. Применение параметризованных классов

Параметризованные классы используются для создания универсальных структур данных и повышения переиспользуемости кода. Например, можно создать класс, представляющий контейнер для любого типа данных.

#### Пример использования

```java
public class Main {
    public static void main(String[] args) {
        // Создание экземпляра параметризованного класса для Integer
        GenericClass<Integer> intBox = new GenericClass<>(123);
        System.out.println("Integer value: " + intBox.getData());

        // Создание экземпляра параметризованного класса для String
        GenericClass<String> strBox = new GenericClass<>("Hello, Generics!");
        System.out.println("String value: " + strBox.getData());
    }
}
```

### 4. Множественные параметры типа

Вы можете создавать классы, которые принимают несколько параметров типа:

```java
class Pair<K, V> {
    private K key;
    private V value;

    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    public K getKey() {
        return key;
    }

    public V getValue() {
        return value;
    }
}
```

#### Пример использования множественных параметров типа

```java
public class Main {
    public static void main(String[] args) {
        Pair<String, Integer> pair = new Pair<>("Age", 30);
        System.out.println(pair.getKey() + ": " + pair.getValue());
    }
}
```

## Ограничения параметризованных классов

Вы можете указывать ограничения на типы, которые могут использоваться в параметризованных классах:

### Пример с верхней границей

```java
class NumberBox<T extends Number> {
    private T number;

    public NumberBox(T number) {
        this.number = number;
    }

    public double doubleValue() {
        return number.doubleValue();
    }
}
```

### Использование

```java
public class Main {
    public static void main(String[] args) {
        NumberBox<Integer> intBox = new NumberBox<>(10);
        System.out.println("Double value: " + intBox.doubleValue());
        
        NumberBox<Double> doubleBox = new NumberBox<>(15.5);
        System.out.println("Double value: " + doubleBox.doubleValue());
    }
}
```

## Заключение

Параметризованные классы в Java предоставляют мощный механизм для создания гибкого и безопасного кода. Используя дженерики, вы можете создавать универсальные структуры данных и писать переиспользуемые алгоритмы, что делает вашу программу более эффективной и легко поддерживаемой.