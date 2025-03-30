---
tags:
  - Spring
  - WEB
---

## Аннотация @PathVariable в Spring MVC

Аннотация `@PathVariable` в Spring MVC используется для извлечения значений из переменных пути URL. Это полезно, когда необходимо передать данные через URL, такие как идентификаторы или другие параметры, и сделать их доступными в методах контроллера.

### Основное назначение

- **Извлечение данных из URL**: Позволяет получать значения переменных, которые указаны в URL как часть маршрута.
- **Улучшение читаемости**: Делает URL более чистыми и семантически значимыми, так как переменные могут быть отражены прямо в URL.

### Синтаксис

Аннотация `@PathVariable` используется в параметрах метода контроллера. Основной синтаксис выглядит следующим образом:

```java
public String methodName(@PathVariable("variableName") Type variableName) {
    // Логика метода
}
```

Если имя переменной в URL совпадает с именем параметра, то можно опустить имя:

```java
public String methodName(@PathVariable Type variableName) {
    // Логика метода
}
```

### Пример использования @PathVariable

Рассмотрим, как использовать аннотацию `@PathVariable` для получения информации о студенте по его идентификатору.

#### 1. Определение контроллера с @PathVariable

```java
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;

@Controller
@RequestMapping("/students")
public class StudentController {

    // Пример метода, извлекающего идентификатор студента из URL
    @RequestMapping(value = "/{id}", method = RequestMethod.GET)
    public String getStudentById(@PathVariable Long id, Model model) {
        // Здесь логика для поиска студента по ID
        Student student = studentService.findById(id);
        model.addAttribute("student", student);
        return "studentDetails"; // Имя представления с деталями студента
    }
}
```

#### 2. Пример HTTP-запроса

Если мы отправим GET-запрос на URL `http://localhost:8080/students/1`, то метод `getStudentById` будет вызван, а переменная `id` будет иметь значение `1`.

### Использование нескольких PathVariable

Можно извлекать несколько переменных сразу.

```java
@RequestMapping(value = "/{studentId}/courses/{courseId}", method = RequestMethod.GET)
public String getStudentCourse(
        @PathVariable Long studentId,
        @PathVariable Long courseId,
        Model model) {
    // Логика для получения курса студента
    // ...
    return "studentCourseDetails"; // Имя представления
}
```

#### HTTP-запрос

Запрос на URL `http://localhost:8080/students/1/courses/101` вызовет метод `getStudentCourse`, передавая `studentId` и `courseId`.

### Комбинирование с @RequestMapping

Аннотация `@PathVariable` может быть использована в методах, помеченных `@RequestMapping`, `@GetMapping`, `@PostMapping`, и другими. Например:

```java
@GetMapping("/students/{id}")
public String fetchStudent(@PathVariable Long id) {
    // Логика получения студента
}
```

### Заключение

Аннотация `@PathVariable` в Spring MVC является мощным инструментом для извлечения переменных из URL-адресов. Использование этой аннотации позволяет создавать более чистые и читаемые маршруты, а также облегчает обработку запросов с динамическими данными. Это делает разработку RESTful API более удобной и интуитивной.