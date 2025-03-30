---
tags:
  - Spring
  - WEB
---

> [!NOTE]
> ## Представление (View) в Spring MVC
> 
> В контексте Spring MVC **представление** (View) отвечает за отображение данных пользователям. Оно формирует пользовательский интерфейс (UI) и использует данные, переданные контроллером, для их визуализации. Spring MVC поддерживает различные технологии для создания представлений, включая JSP, Thymeleaf, FreeMarker и другие.

### Основные компоненты представления

1. **Технологии представления**:
   - JSP (JavaServer Pages)
   - Thymeleaf
   - FreeMarker
   - другие шаблонизаторы

2. **Взаимодействие с моделью**:
   - Представления используют данные модели, переданные контроллером, чтобы динамически отображать информацию.

### 1. JSP (JavaServer Pages)

JSP — это один из самых популярных способов создания представлений в Java-фреймах. JSP-файлы представляют собой HTML-код с вкраплениями Java-кода и выражений. Они позволяют динамически формировать содержимое веб-страниц.

#### Пример JSP-представления

Вот пример JSP-файла `studentList.jsp`, который отображает список студентов:

```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<!DOCTYPE html>
<html>
<head>
    <title>Список студентов</title>
</head>
<body>

<h1>Список студентов</h1>

<form action="${pageContext.request.contextPath}/students/add" method="post">
    <label for="name">Имя студента:</label>
    <input type="text" id="name" name="name" required>
    <button type="submit">Добавить студента</button>
</form>

<ul>
    <c:forEach var="student" items="${students}">
        <li>${student.name}</li>  <!-- Использование EL для доступа к данным -->
    </c:forEach>
</ul>

</body>
</html>
```

### 2. Thymeleaf

**Thymeleaf** — это современный шаблонизатор для Java, который предоставляет значительно более чистый и читабельный код по сравнению с JSP. Thymeleaf упрощает создание динамических веб-страниц с поддержкой полного HTML.

#### Пример Thymeleaf-представления

Вот пример файла `studentList.html` с использованием Thymeleaf:

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Список студентов</title>
</head>
<body>

<h1>Список студентов</h1>

<form th:action="@{/students/add}" method="post">
    <label for="name">Имя студента:</label>
    <input type="text" id="name" name="name" required>
    <button type="submit">Добавить студента</button>
</form>

<ul>
    <li th:each="student : ${students}" th:text="${student.name}">Имя студента</li>
</ul>

</body>
</html>
```

### 3. FreeMarker

**FreeMarker** — это ещё один шаблонизатор, который позволяет динамически генерировать HTML-страницы, письма и другие текстовые файлы. Он поддерживает шаблоны и предоставляет мощные возможности для обработки данных.

#### Пример FreeMarker-представления

Пример файла `studentList.ftl`:

```ftl
<!DOCTYPE html>
<html>
<head>
    <title>Список студентов</title>
</head>
<body>

<h1>Список студентов</h1>

<form action="/students/add" method="post">
    <label for="name">Имя студента:</label>
    <input type="text" id="name" name="name" required>
    <button type="submit">Добавить студента</button>
</form>

<ul>
<#list students as student>
    <li>${student.name}</li>
</#list>
</ul>

</body>
</html>
```

### Взаимодействие представления с контроллером

Представление получает данные из модели, которые контроллер передает через объект `Model`. Контроллер заполняет модель данными, а затем возвращает имя представления.

#### Пример контроллера:

```java
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
        model.addAttribute("students", students); // Передаем список студентов в модель
        return "studentList"; // Имя JSP или Thymeleaf представления
    }
}
```

### Конфигурация представлений

Для определения, какой шаблонизатор использовать и где искать представления, нужно настроить `view resolver` в конфигурации Spring.

#### Пример конфигурации `InternalResourceViewResolver` для JSP:

```xml
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/views/" /> <!-- Папка с представлениями -->
    <property name="suffix" value=".jsp" />
</bean>
```

#### Пример конфигурации для Thymeleaf:

```java
@Bean
public SpringTemplateEngine templateEngine() {
    SpringTemplateEngine engine = new SpringTemplateEngine();
    engine.setTemplateResolver(templateResolver());
    return engine;
}

@Bean
public TemplateResolver templateResolver() {
    TemplateResolver resolver = new SpringResourceTemplateResolver();
    resolver.setPrefix("/templates/");
    resolver.setSuffix(".html");
    resolver.setTemplateMode("HTML");
    return resolver;
}
```

### Заключение

Представление в Spring MVC отвечает за отображение данных пользователям и является важным элементом архитектуры MVC. Различные технологии представления, такие как JSP, Thymeleaf и FreeMarker, предоставляют разработчикам гибкость в создании пользовательских интерфейсов. Правильная организация представлений и их взаимодействие с контроллерами обеспечивает создание удобных, интуитивных и динамических веб-приложений.