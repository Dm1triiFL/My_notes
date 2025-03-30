---
tags:
  - "#Pattern"
---
## Builder Pattern

**Builder Pattern** — это паттерн проектирования, используемый для создания сложных объектов. Он отделяет процесс создания объект от его представления, что позволяет создавать разные представления одного и того же объекта. Данный паттерн особенно полезен, когда объект имеет множество параметров, некоторые из которых могут быть необязательными.

### Основные характеристики

1. **Отделение построения объекта от его представления**:
   - Позволяет создавать различные представления объектов при помощи одного и того же процесса построения.

2. **Улучшение читаемости кода**:
   - За счет цепочечного вызова методов создание объектов становится более понятным и удобным.

3. **Поддержка неизменяемости**:
   - Позволяет создавать неизменяемые объекты, что важно для безопасности и управления состоянием.

### Основная структура

Builder Pattern обычно включает в себя следующие компоненты:

- **Builder**: интерфейс или абстрактный класс, определяющий абстрактные методы для создания частей объекта.
- **ConcreteBuilder**: конкретная реализация интерфейса Builder, которая управляет процессом создания и предоставляет итоговый объект.
- **Director**: класс, который управляет построением объектов и использует Builder для создания составных частей объекта.
- **Product**: конечный объект, который создается.

### Пример реализации на Java

Рассмотрим пример реализации Builder Pattern в Java.

1. **Создание класса `Product`**:

```java
public class User {
    private final String username; // Обязательный параметр
    private final String email;     // Обязательный параметр
    private final String phone;     // Необязательный параметр

    private User(UserBuilder builder) {
        this.username = builder.username;
        this.email = builder.email;
        this.phone = builder.phone;
    }

    // Геттеры
    public String getUsername() {
        return username;
    }

    public String getEmail() {
        return email;
    }

    public String getPhone() {
        return phone;
    }

    // Статический класс Builder
    public static class UserBuilder {
        private final String username; // Обязательный параметр
        private final String email;     // Обязательный параметр
        private String phone;           // Необязательный параметр

        public UserBuilder(String username, String email) {
            this.username = username;
            this.email = email;
        }

        public UserBuilder phone(String phone) {
            this.phone = phone;
            return this;
        }

        public User build() {
            return new User(this);
        }
    }
}
```

2. **Использование Builder**:

```java
public class Main {
    public static void main(String[] args) {
        User user = new User.UserBuilder("johndoe", "john.doe@example.com")
                                .phone("123-456-7890")
                                .build();

        System.out.println("Username: " + user.getUsername());
        System.out.println("Email: " + user.getEmail());
        System.out.println("Phone: " + user.getPhone());
    }
}
```

### Объяснение примера

1. **Класс `User`**:
   - Содержит обязательные (`username`, `email`) и необязательный (`phone`) параметры, которые определяются через внутренний класс `UserBuilder`.

2. **Класс `UserBuilder`**:
   - Имеет методы для установки параметров и метод `build()`, который создает и возвращает объект `User`.

3. **Использование `Builder`**:
   - Создание объекта `User` происходит через вызов методов `UserBuilder`, что улучшает читаемость и управляемость кода.

### Заключение

Builder Pattern предлагает мощный способ создания объектов с многоуровневыми и комплексными конфигурациями. Он улучшает читаемость кода, поддерживает неизменяемость объектов и дает возможность создавать различные представления одного и того же объекта. Этот паттерн особенно полезен в сложных системах, где объекты имеют множество параметров, из которых некоторые могут быть необязательными.

[[Аннотация Builder]]