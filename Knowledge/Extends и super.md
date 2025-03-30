---
tags:
  - Java
---
# Использование `extends` и `super` в дженериках (Generics) в Java

В Java дженерики позволяют создавать классы, интерфейсы и методы, которые работают с параметризованными типами. При этом можно использовать ключевые слова `extends` и `super` для задания ограничений на параметры типа.

## 1. Ключевое слово `extends`

### Определение
Ключевое слово `extends` в дженериках применяется для указания верхней границы (bounded type) параметра типа. Это позволяет ограничить тип, который может быть использован.

### Синтаксис
```java
public class ClassName<T extends SomeClass> {
    // Класс может использовать T, который является подклассом SomeClass
}
```

### Пример
```java
class Animal { }
class Dog extends Animal { }
class Cat extends Animal { }

public class AnimalShelter<T extends Animal> {
    private T animal;

    public void setAnimal(T animal) {
        this.animal = animal;
    }

    public T getAnimal() {
        return animal;
    }
}

// Применение
AnimalShelter<Dog> dogShelter = new AnimalShelter<>();
dogShelter.setAnimal(new Dog());
```

### Примечание
- `extends` может использоваться как для классов, так и для интерфейсов.
- Вы можете указать несколько границ, используя `&`:
  ```java
  public class SomeClass<T extends ClassA & InterfaceB> { }
  ```

## 2. Ключевое слово `super`

### Определение
Ключевое слово `super` в дженериках используется для указания нижней границы (lower bound) параметра типа. Оно позволяет использовать типы, которые являются суперклассами заданного типа.

### Синтаксис
```java
public void methodName(List<? super SomeClass> list) {
    // Метод может принимать список, элементы которого являются суперклассами SomeClass
}
```

### Пример
```java
public void addAnimal(List<? super Dog> list) {
    list.add(new Dog());
}

// Применение
ArrayList<Animal> animals = new ArrayList<>();
addAnimal(animals);
```

### Примечание
- `super` обычно используется в методах, когда мы хотим добавлять элементы в коллекции, а не извлекать их.
- Для извлечения элементов из обобщенного метода лучше использовать `extends`.

## Заключение

- Используйте **`extends`** для определения верхней границы и ограничения типов, которые могут использоваться в дженериках.
- Используйте **`super`** для определения нижней границы, что позволяет добавлять объекты в коллекции.

