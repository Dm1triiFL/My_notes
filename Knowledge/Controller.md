---
tags:
  - Spring
  - WEB
---
## Контроллеры в Spring MVC: подробное руководство

Контроллеры в Spring MVC являются центральными компонентами, управляющими маршрутами, логикой обработки запросов и взаимодействием между моделью и представлением. В этом разделе мы рассмотрим более подробно, как работают контроллеры, их аннотации, жизненный цикл и примеры их использования.

### Основные аннотации для контроллеров

#### 1. @Controller

Эта аннотация используется для объявления класса как контроллера. Spring будет управлять экземплярами этого класса, что позволяет ему обрабатывать HTTP-запросы.

#### 2. @RequestMapping

Эта аннотация позволяет задавать URL-адреса, к которым будет привязан метод контроллера. Она может быть использована на уровне класса или метода.

##### Пример использования:

```java
@Controller
@RequestMapping("/students") // Базовый URL для всех методов в классе
public class StudentController {
    // Методы контроллера
}
```

#### 3. @GetMapping и @PostMapping

Эти аннотации обеспечивают удобный способ обработки HTTP GET и POST запросов соответственно.

- **@GetMapping**: используется, чтобы обрабатывать GET-запросы.

- **@PostMapping**: используется для обработки POST-запросов.

##### Пример:

```java
@GetMapping
public String showStudents() {
    // Обработка GET-запроса
}

@PostMapping
public String addStudent(@RequestParam String name) {
    // Обработка POST-запроса
}
```

### Инъекция зависимостей

Spring MVC поддерживает инъекцию зависимостей, что позволяет контроллерам получать необходимые сервисы и репозитории через конструктор или поля.

#### Пример инъекции зависимостей:

```java
@Controller
@RequestMapping("/students")
public class StudentController {

    private final StudentService studentService;

    // Конструктор для инъекции зависимости
    @Autowired
    public StudentController(StudentService studentService) {
        this.studentService = studentService;
    }

    @GetMapping
    public String listStudents(Model model) {
        List<Student> students = studentService.findAll();
        model.addAttribute("students", students);
        return "studentList";
    }
}
```

### Обработка параметров и состояния модели

Контроллеры могут обрабатывать параметры запроса и передавать данные в представление с помощью объекта `Model`.

#### Обработка параметров:

- **@RequestParam**: используется для извлечения параметров из URL.
- **@PathVariable**: позволяет извлекать данные из URI.

##### Пример:

```java
@GetMapping("/{id}")
public String getStudentById(@PathVariable Long id, Model model) {
    Student student = studentService.findById(id);
    model.addAttribute("student", student);
    return "studentDetails";
}
```

### Управление откликами

Контроллеры могут возвращать разные типы ответов, такие как представления, JSON или даже строки. Благодаря аннотации `@ResponseBody`, можно вернуть данные, которые будут сериализованы в JSON.

#### Пример возврата JSON:

```java
@GetMapping("/api/students")
@ResponseBody // Указывает, что результат будет сериализован в JSON
public List<Student> getAllStudents() {
    return studentService.findAll();
}
```

### Обработка ошибок

Spring MVC предоставляет возможность обработки ошибок через аннотацию `@ExceptionHandler`, позволяя вам управлять исключениями, возникающими в контроллерах.

#### Пример обработки исключений:

```java
@Controller
@RequestMapping("/students")
public class StudentController {

    // Другие методы

    @ExceptionHandler(StudentNotFoundException.class)
    public String handleStudentNotFound(StudentNotFoundException ex, Model model) {
        model.addAttribute("errorMessage", ex.getMessage());
        return "error"; // Отображение страницы с сообщением об ошибке
    }
}
```

### Полный пример контроллера

Теперь мы соберем все эти идеи в один интегрированный образец контроллера:

```java
package com.example.controller;

import com.example.model.Student;
import com.example.service.StudentService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@Controller
@RequestMapping("/students")
public class StudentController {

    private final StudentService studentService;

    @Autowired
    public StudentController(StudentService studentService) {
        this.studentService = studentService;
    }

    @GetMapping
    public String listStudents(Model model) {
        List<Student> students = studentService.findAll();
        model.addAttribute("students", students);
        return "studentList";
    }

    @GetMapping("/{id}")
    public String getStudentById(@PathVariable Long id, Model model) {
        Student student = studentService.findById(id);
        model.addAttribute("student", student);
        return "studentDetails";
    }

    @PostMapping("/add")
    public String addStudent(@RequestParam String name) {
        studentService.addStudent(new Student(name));
        return "redirect:/students";
    }

    @ExceptionHandler(StudentNotFoundException.class)
    public String handleStudentNotFound(StudentNotFoundException ex, Model model) {
        model.addAttribute("errorMessage", ex.getMessage());
        return "error";
    }
}
```

### Заключение

Контроллеры в Spring MVC являются основой для построения веб-приложений, связывая модель и представление. Понимание аннотаций, способностей обработки HTTP-запросов, управления зависимостями и обработки ошибок позволяет создавать более эффективные и структурированные приложения. Используя эти концепции, разработчики могут гибко строить взаимодействия с пользователями, обеспечивая удобство и функциональность веб-приложений.