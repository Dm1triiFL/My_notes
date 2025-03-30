---
tags:
  - Java
---
# Wildcards в Java

**Wildcards** (подстановочные знаки) в Java используются в обобщенных (generic) классах и методах для представления неопределенного типа. Это позволяет создавать более гибкие и мощные обобщенные конструкции.

## 1. Что такое Wildcards?

Wildcards обозначаются знаком вопроса (`?`) и используются для обозначения неизвестного типа. Чаще всего они применяются в методах и при работе с коллекциями.

### Основные типы Wildcards:
- **Unbounded Wildcards**: Обозначается как `?`
- **Upper Bounded Wildcards**: Обозначается как `? extends Type`
- **Lower Bounded Wildcards**: Обозначается как `? super Type`

## 2. Применение Wildcards

### 2.1. Unbounded Wildcards (`?`)
Используется, когда тип не важен. Например, в методах, где коллекция может содержать любые типы.

**Пример:**
```java
public void printList(List<?> list) {
    for (Object elem : list) {
        System.out.println(elem);
    }
}
```

### 2.2. Upper Bounded Wildcards (`? extends Type`)
Ограничивает тип, позволяя использовать только подтипы указанного класса.

**Пример:**
```java
public void addAnimal(List<? extends Animal> animals) {
    // Можно только читать из animals, а не добавлять
}
```

### 2.3. Lower Bounded Wildcards (`? super Type`)
Ограничивает тип, позволяя использовать только суперклассы указанного класса. Это полезно, когда необходимо добавлять элементы в коллекцию.

**Пример:**
```java
public void addDog(List<? super Dog> dogs) {
    dogs.add(new Dog());
}
```

## 3. Пример использования Wildcards

```java
class Animal { }
class Dog extends Animal { }
class Cat extends Animal { }

public class WildcardExample {
    public static void processAnimals(List<? extends Animal> animals) {
        for (Animal animal : animals) {
            System.out.println(animal);
        }
    }
    
    public static void addAnimal(List<? super Dog> dogs) {
        dogs.add(new Dog());
    }
}
```

## Заключение

Wildcards обеспечивают гибкость и позволяют создавать более универсальные методы и классы в Java. Понимание, как и когда использовать каждый из типов Wildcards, важно для эффективного программирования на Java. Если у вас есть дополнительные вопросы или примеры, которые вы хотели бы увидеть, не стесняйтесь спрашивать!