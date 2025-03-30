---
tags:
  - Spring
  - WEB
---

## Аннотация @ModelAttribute в Spring MVC

Аннотация `@ModelAttribute` используется в Spring MVC для связывания данных из HTTP-запроса с объектом модели. Это позволяет легко передавать данные между представлениями и контроллерами, что особенно полезно для работы с формами и автозаполнением объектов.

### Основные функции @ModelAttribute

1. **Автоматическое связывание данных**: Автоматически связывает параметры из строки запроса с полями объекта модели.
2. **Поддержка форм**: Упрощает обработку форм, автоматически заполняя поля объекта на основе переданных данных.
3. **Подготовка данных для представления**: Может использоваться для подготовки данных модели, передаваемых в представление.

### Синтаксис

`@ModelAttribute` может быть использована как на уровне метода контроллера, так и на уровне параметра метода. 

#### Уровень метода

Когда используется на уровне метода, объект модифицируется и добавляется в модель, чтобы быть доступным во представлении.

```java
@ModelAttribute
public void addAttributes(Model model) {
    model.addAttribute("attributeName", attributeValue);
}
```

#### Уровень параметра

Когда используется на уровне параметра, Spring автоматически связывает данные из запроса с объектом:

```java
public String submitForm(@ModelAttribute MyForm myForm) {
    // Обработка данных формы
    return "formResult";
}
```

### Примеры использования @ModelAttribute

#### 1. Пример связывания данных из формы

Предположим, у вас есть форма для ввода данных о студенте.

```java
public class Student {
    private Long id;
    private String name;
    private int age;

    // Геттеры и сеттеры
}
```

Контроллер для обработки формы:

```java
@Controller
@RequestMapping("/students")
public class StudentController {

    @GetMapping("/new")
    public String showStudentForm(Model model) {
        model.addAttribute("student", new Student()); // Пустой объект для формы
        return "studentForm"; // Название представления
    }

    @PostMapping("/submit")
    public String submitForm(@ModelAttribute Student student) {
        // Логика для обработки студента
        return "redirect:/students"; // Перенаправление
    }
}
```

##### Пример представления `studentForm.jsp`

```jsp
<form action="${pageContext.request.contextPath}/students/submit" method="post">
    <input type="text" name="name" placeholder="Имя" required>
    <input type="number" name="age" placeholder="Возраст" required>
    <button type="submit">Добавить студента</button>
</form>
```

При отправке формы данные автоматически связываются с объектом `Student`, и поля `name` и `age` заполняются на основе значений, введённых в форме.

#### 2. Пример подготовки данных для представления

Также `@ModelAttribute` можно использовать для добавления общих атрибутов в модель, чтобы они были доступны во всех методах контроллера.

```java
@ModelAttribute
public void addCommonAttributes(Model model) {
    model.addAttribute("commonAttribute", "Общее значение");
}
```

Эти атрибуты будут автоматически доступны во всех представлениях, обрабатываемых этим контроллером.

### Заключение

Аннотация `@ModelAttribute` в Spring MVC является мощным инструментом для обработки данных форм и связывания их с объектами модели. Она упрощает разработку и ускоряет процесс обработки пользовательского ввода, улучшая взаимодействие между контроллерами и представлениями. Правильное использование `@ModelAttribute` способствует более чистому и читаемому коду, делая приложения более удобными в сопровождении и масштабировании.