---
tags:
  - Spring
---
## Создание простого Spring Boot приложения

### 1. Создание нового проекта

Вы можете использовать [Spring Initializr](https://start.spring.io/) для создания нового проекта. Выберите следующие зависимости:

- **Spring Web**
- **Spring Data JPA**
- **H2 Database** (или другую базу данных по вашему выбору)

### 2. Структура проекта

После создания проектной структуры вы получите что-то подобное:

```
src/main/java/com/example/demo/
├── DemoApplication.java
├── controller
│   └── HelloController.java
├── model
│   └── User.java
└── repository
    └── UserRepository.java
```

### 3. Создание основного класса (DemoApplication.java)

Создайте класс, который будет запускать ваше приложение.

```java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

### 4. Создание модели пользователя (User.java)

Создайте класс модели для представления сущности.

```java
package com.example.demo.model;

import javax.persistence.*;

@Entity
@Table(name = "users")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;

    // Геттеры и сеттеры
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
```

### 5. Создание репозитория (UserRepository.java)

Создайте интерфейс репозитория для работы с данными.

```java
package com.example.demo.repository;

import com.example.demo.model.User;
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
}
```

### 6. Создание контроллера (HelloController.java)

Создайте контроллер для обработки HTTP-запросов.

```java
package com.example.demo.controller;

import com.example.demo.model.User;
import com.example.demo.repository.UserRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/api/users")
public class UserController {

    @Autowired
    private UserRepository userRepository;

    @GetMapping
    public List<User> getAllUsers() {
        return userRepository.findAll();
    }

    @PostMapping
    public User createUser(@RequestBody User user) {
        return userRepository.save(user);
    }
}
```

### 7. Настройка базы данных

Создайте файл `application.properties` в `src/main/resources` для настройки H2 Database:

```properties
# Настройки H2 Database
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.h2.console.enabled=true
spring.jpa.hibernate.ddl-auto=update
```

### 8. Запуск приложения

Теперь вы можете запустить приложение. Откройте класс `DemoApplication.java` и выполните его.

### 9. Тестирование API

Вы можете использовать Postman или другой инструмент для отправки HTTP-запросов и тестирования API.

#### Примеры запросов

1. **GET /api/users**:
   - Получает список всех пользователей.

2. **POST /api/users**:
   - Создает нового пользователя.
   - Пример тела запроса:
     ```json
     {
         "name": "John Doe",
         "email": "john.doe@example.com"
     }
     ```
### Заключение

Вы создали простое приложение на Spring Boot, включающее работу с REST API, базами данных и автоматической конфигурацией. Spring Boot позволяет легко разрабатывать и развертывать приложения, обеспечивая мощные инструменты и функции для разработчиков. Это приложение можно расширить, добавляя дополнительные функциональности и интеграции в зависимости от ваших потребностей.