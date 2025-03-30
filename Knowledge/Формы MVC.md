---
tags:
  - Spring
  - WEB
---
# Примеры форм в Spring MVC

Ниже приведены примеры использования различных типов ввода в формах Spring MVC: `input`, `select` и `checkbox`. Каждый пример включает элемент формы, контроллер и представление.

## 1. Spring MVC Форма с Input

### Модель

```java
public class Student {
    private String name;
    private int age;

    // Геттеры и сеттеры
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

### Контроллер

```java
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.ModelAttribute;

@Controller
@RequestMapping("/students")
public class StudentController {

    @GetMapping("/new")
    public String showStudentForm(Model model) {
        model.addAttribute("student", new Student());
        return "studentForm";
    }

    @PostMapping("/submit")
    public String submitForm(@ModelAttribute Student student) {
        // Логика обработки данных студента
        return "redirect:/students"; // Перенаправление после сохранения
    }
}
```

### Представление (`studentForm.jsp`)

```jsp
<%@ taglib uri="http://www.springframework.org/tags/form" prefix="form" %>
<!DOCTYPE html>
<html>
<head>
    <title>Добавить студента</title>
</head>
<body>
<h2>Добавить студента</h2>
<form:form method="post" modelAttribute="student" action="${pageContext.request.contextPath}/students/submit">
    <label for="name">Имя:</label>
    <form:input path="name" id="name" required="true" />
    <br>
    <label for="age">Возраст:</label>
    <form:input path="age" id="age" type="number" required="true" />
    <br>
    <button type="submit">Добавить студента</button>
</form:form>
</body>
</html>
```

---

## 2. Spring MVC Форма с Select

### Модель

```java
public class Student {
    private String name;
    private String country;

    // Геттеры и сеттеры
    // ...
}
```

### Контроллер

```java
@Controller
@RequestMapping("/students")
public class StudentController {

    @GetMapping("/new")
    public String showStudentForm(Model model) {
        model.addAttribute("student", new Student());
        model.addAttribute("countries", new String[]{"Россия", "США", "Германия", "Франция"});
        return "studentForm";
    }

    @PostMapping("/submit")
    public String submitForm(@ModelAttribute Student student) {
        // Логика обработки данных студента
        return "redirect:/students"; 
    }
}
```

### Представление (`studentForm.jsp`)

```jsp
<%@ taglib uri="http://www.springframework.org/tags/form" prefix="form" %>
<!DOCTYPE html>
<html>
<head>
    <title>Добавить студента</title>
</head>
<body>
<h2>Добавить студента</h2>
<form:form method="post" modelAttribute="student" action="${pageContext.request.contextPath}/students/submit">
    <label for="name">Имя:</label>
    <form:input path="name" id="name" required="true" />
    <br>
    <label for="country">Страна:</label>
    <form:select path="country" id="country">
        <form:option value="" label="Выберите страну" />
        <c:forEach var="country" items="${countries}">
            <form:option value="${country}">${country}</form:option>
        </c:forEach>
    </form:select>
    <br>
    <button type="submit">Добавить студента</button>
</form:form>
</body>
</html>
```

---

## 3. Spring MVC Форма с Checkbox

### Модель

```java
public class Student {
    private String name;
    private boolean newsletterSubscription;

    // Геттеры и сеттеры
    // ...
}
```

### Контроллер

```java
@Controller
@RequestMapping("/students")
public class StudentController {

    @GetMapping("/new")
    public String showStudentForm(Model model) {
        model.addAttribute("student", new Student());
        return "studentForm";
    }

    @PostMapping("/submit")
    public String submitForm(@ModelAttribute Student student) {
        // Логика обработки данных студента
        return "redirect:/students"; 
    }
}
```

### Представление (`studentForm.jsp`)

```jsp
<%@ taglib uri="http://www.springframework.org/tags/form" prefix="form" %>
<!DOCTYPE html>
<html>
<head>
    <title>Добавить студента</title>
</head>
<body>
<h2>Добавить студента</h2>
<form:form method="post" modelAttribute="student" action="${pageContext.request.contextPath}/students/submit">
    <label for="name">Имя:</label>
    <form:input path="name" id="name" required="true" />
    <br>
    <label for="newsletterSubscription">Подписка на рассылку:</label>
    <form:checkbox path="newsletterSubscription" id="newsletterSubscription" />
    <br>
    <button type="submit">Добавить студента</button>
</form:form>
</body>
</html>
```

---

## Заключение

Эти примеры показывают, как создать формы с различными элементами ввода в Spring MVC, используя аннотацию `@ModelAttribute` для связывания данных с объектом модели. Формы `input`, `select` и `checkbox` легко интегрируются и обеспечивают удобный интерфейс для пользователей.