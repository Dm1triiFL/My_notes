---
tags:
  - Spring
  - WEB
---

# Пример REST приложения на Spring Boot

Давайте создадим простое REST API-приложение с использованием Spring Boot. В этом приложении мы будем управлять ресурсами студентов, включая операции для создания, чтения, обновления и удаления (CRUD).

## Шаги создания REST приложения

### 1. Создание нового проекта Spring Boot

Вы можете использовать Spring Initializr для создания нового проекта. Включите следующие зависимости:

- **Spring Web**
- **Spring Data JPA**
- **H2 Database** (для тестирования)

### 2. Настройка проекта

Выберите настройки проекта и загрузите ZIP-файл. Затем распакуйте и импортируйте проект в вашу IDE.

### 3. Структура проекта

После создания проекта структура вашего проекта должна выглядеть следующим образом:

```
src/main/java/com/example/restapi/
├── RestApiApplication.java
├── controller
│   └── StudentController.java
├── model
│   └── Student.java
└── repository
    └── StudentRepository.java
```

### 4. Создание модели (Student.java)

Создайте класс модели, который будет представлять студента.

```java
package com.example.restapi.model;

import javax.persistence.*;

@Entity
@Table(name = "students")
public class Student {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private int age;

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

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

### 5. Создание репозитория (StudentRepository.java)

Создайте интерфейс репозитория, который будет расширять `JpaRepository`.

```java
package com.example.restapi.repository;

import com.example.restapi.model.Student;
import org.springframework.data.jpa.repository.JpaRepository;

public interface StudentRepository extends JpaRepository<Student, Long> {
}
```

### 6. Создание контроллера (StudentController.java)

Создайте REST контроллер для обработки запросов.

```java
package com.example.restapi.controller;

import com.example.restapi.model.Student;
import com.example.restapi.repository.StudentRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/api/students")
public class StudentController {

    @Autowired
    private StudentRepository studentRepository;

    // Получить всех студентов
    @GetMapping
    public List<Student> getAllStudents() {
        return studentRepository.findAll();
    }

    // Получить студента по ID
    @GetMapping("/{id}")
    public ResponseEntity<Student> getStudentById(@PathVariable Long id) {
        return studentRepository.findById(id)
                .map(student -> ResponseEntity.ok(student))
                .orElse(ResponseEntity.notFound().build());
    }

    // Создать нового студента
    @PostMapping
    public Student createStudent(@RequestBody Student student) {
        return studentRepository.save(student);
    }

    // Обновить студента
    @PutMapping("/{id}")
    public ResponseEntity<Student> updateStudent(@PathVariable Long id, @RequestBody Student studentData) {
        return studentRepository.findById(id)
                .map(student -> {
                    student.setName(studentData.getName());
                    student.setAge(studentData.getAge());
                    Student updatedStudent = studentRepository.save(student);
                    return ResponseEntity.ok(updatedStudent);
                })
                .orElse(ResponseEntity.notFound().build());
    }

    // Удалить студента
    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteStudent(@PathVariable Long id) {
        return studentRepository.findById(id)
                .map(student -> {
                    studentRepository.delete(student);
                    return ResponseEntity.noContent().build();
                })
                .orElse(ResponseEntity.notFound().build());
    }
}
```

### 7. Настройка базы данных

Создайте файл `application.properties` в `src/main/resources` для настройки H2 Database.

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

Теперь вы можете запустить приложение. Откройте класс `RestApiApplication.java` и выполните его.

### 9. Тестирование API

Вы можете использовать Postman или любой другой инструмент для тестирования REST API.

#### Примеры запросов

1. **GET /api/students**
   - Получить всех студентов.

2. **GET /api/students/{id}**
   - Получить студента по ID.

3. **POST /api/students**
   - Создать нового студента.
   - Пример тела запроса:
     ```json
     {
         "name": "John Doe",
         "age": 21
     }
     ```

4. **PUT /api/students/{id}**
   - Обновить информацию о студенте по ID.
   - Пример тела запроса:
     ```json
     {
         "name": "Jane Doe",
         "age": 25
     }
     ```

5. **DELETE /api/students/{id}**
   - Удалить студента по ID.

### Заключение

Вы создали простое REST API-приложение на Spring Boot для управления ресурсами студентов. Используя Spring Data JPA, вы смогли легко реализовать операции CRUD. Это приложение можно расширять, добавляя дополнительные функции и услуги в зависимости от ваших потребностей.