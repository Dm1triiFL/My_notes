---
tags:
  - Spring
  - WEB
---
## Интеграция Service Layer в Spring MVC и Hibernate

Добавление уровня сервиса в приложение на основе Spring MVC и Hibernate обеспечивает более организованную структуру, которая помогает управлять бизнес-логикой и взаимодействием с данными. Это позволяет изолировать бизнес-логику от контроллеров и упрощает тестирование приложения.

### 1. Создание сервиса

Создайте интерфейс и его реализацию для управления данными сущности `Student`.

#### StudentService

```java
package com.example.service;

import com.example.model.Student;
import java.util.List;

public interface StudentService {
    void saveStudent(Student student);
    List<Student> listStudents();
}
```

#### StudentServiceImpl

```java
package com.example.service;

import com.example.model.Student;
import com.example.dao.StudentDAO;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import java.util.List;

@Service
public class StudentServiceImpl implements StudentService {

    @Autowired
    private StudentDAO studentDAO;

    @Transactional
    @Override
    public void saveStudent(Student student) {
        studentDAO.saveStudent(student);
    }

    @Transactional(readOnly = true)
    @Override
    public List<Student> listStudents() {
        return studentDAO.listStudents();
    }
}
```

### 2. Обновление DAO с использованием @Transactional

Добавьте аннотацию `@Transactional` в методы DAO, чтобы обеспечить управление транзакциями:

#### Обновленный StudentDAOImpl

```java
package com.example.dao;

import com.example.model.Student;
import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Repository;

import java.util.List;

@Repository
public class StudentDAOImpl implements StudentDAO {

    @Autowired
    private SessionFactory sessionFactory;

    @Transactional
    @Override
    public void saveStudent(Student student) {
        Session session = sessionFactory.getCurrentSession();
        session.saveOrUpdate(student);
    }

    @SuppressWarnings("unchecked")
    @Transactional(readOnly = true)
    @Override
    public List<Student> listStudents() {
        Session session = sessionFactory.getCurrentSession();
        return session.createQuery("from Student").list();
    }
}
```

### 3. Обновление контроллера

Измените контроллер, чтобы он использовал уровень сервиса вместо DAO напрямую.

#### Обновленный StudentController

```java
package com.example.controller;

import com.example.service.StudentService;
import com.example.model.Student;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.ModelAttribute;

import java.util.List;

@Controller
@RequestMapping("/students")
public class StudentController {

    @Autowired
    private StudentService studentService;

    @GetMapping("/new")
    public String showForm(Model model) {
        model.addAttribute("student", new Student());
        return "studentForm"; // Представление для формы
    }

    @PostMapping("/submit")
    public String submitForm(@ModelAttribute Student student) {
        studentService.saveStudent(student);
        return "redirect:/students/list"; // Перенаправление на список студентов
    }
    
    @GetMapping("/list")
    public String listStudents(Model model) {
        List<Student> students = studentService.listStudents();
        model.addAttribute("students", students);
        return "studentList"; // Представление для списка студентов
    }
}
```

### 4. Полная структура проекта

Теперь структура вашего проекта должна выглядеть следующим образом:

```
src/main/java/com/example/
├── config
│   └── WebConfig.java
├── controller
│   └── StudentController.java
├── dao
│   ├── StudentDAO.java
│   └── StudentDAOImpl.java
├── model
│   └── Student.java
└── service
    ├── StudentService.java
    └── StudentServiceImpl.java
src/main/resources/
└── hibernate.cfg.xml
```

### 5. Представления

#### `studentForm.jsp`

Останется без изменений:

```jsp
<%@ taglib uri="http://www.springframework.org/tags/form" prefix="form" %>
<!DOCTYPE html>
<html>
<head>
    <title>Добавить студента</title>
</head>
<body>
<h2>Добавить студента</h2>
<form:form modelAttribute="student" method="post" action="${pageContext.request.contextPath}/students/submit">
    <label>Имя:</label>
    <form:input path="name" />
    <br/>
    <label>Возраст:</label>
    <form:input path="age" type="number" />
    <br/>
    <button type="submit">Добавить</button>
</form:form>
</body>
</html>
```

#### `studentList.jsp`

Также останется без изменений:

```jsp
<%@ taglib uri="http://www.springframework.org/tags/form" prefix="form" %>
<!DOCTYPE html>
<html>
<head>
    <title>Список студентов</title>
</head>
<body>
<h2>Список студентов</h2>
<table>
    <tr>
        <th>ID</th>
        <th>Имя</th>
        <th>Возраст</th>
    </tr>
    <c:forEach var="student" items="${students}">
        <tr>
            <td>${student.id}</td>
            <td>${student.name}</td>
            <td>${student.age}</td>
        </tr>
    </c:forEach>
</table>
</body>
</html>
```

### Заключение

Добавление уровня сервиса в ваше приложение на Spring MVC и Hibernate улучшает организацию кода и поддерживаемость системы. Это позволяет вам четко отделять бизнес-логику от логики контроллеров и управления данными, что делает приложение более структурированным и удобным для тестирования.