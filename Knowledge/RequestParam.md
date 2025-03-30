---
tags:
  - Spring
  - WEB
---

> [!info]
> ## Аннотация @RequestParam в Spring MVC
> 
> Аннотация `@RequestParam` используется в Spring MVC для извлечения параметров из строки запроса (query string) HTTP-запроса. Это позволяет контроллерам получать данные, передаваемые через URL, что удобно для работы с формами, фильтрами и другими опциональными параметрами.

### Основные функции @RequestParam

1. **Извлечение значений**: Позволяет получать значения параметров запроса по имени.
2. **Обработка опциональных параметров**: Предоставляет возможность определить, является ли параметр обязательным или опциональным.
3. **Преобразование типов**: Автоматически конвертирует параметры из строкового формата в нужные типы (например, `int`, `Long`, `Date` и др.).

### Синтаксис

Аннотация `@RequestParam` используется в качестве параметра метода контроллера. Основной синтаксис:

```java
public String methodName(@RequestParam("parameterName") String parameterValue) {
    // Логика метода
}
```

Если имя параметра совпадает с именем переменной, можно опустить имя параметра:

```java
public String methodName(@RequestParam String parameterValue) {
    // Логика метода
}
```

### Примеры использования @RequestParam

#### 1. Обязательные параметры

```java
@GetMapping("/students")
public String getStudent(@RequestParam String id) {
    // Логика для получения студента по ID
    return "studentDetails";
}
```

##### Пример URL:

- URL: `http://localhost:8080/students?id=1`
- В данном случае `id` будет равно `1`.

#### 2. Опциональные параметры

Можно указать, является ли параметр опциональным с помощью атрибута `required`.

```java
@GetMapping("/students")
public String searchStudents(@RequestParam(required = false) String name) {
    // Логика для поиска студентов по имени
    return "studentList";
}
```

##### Пример URL:

- URL: `http://localhost:8080/students?name=John`
- В этом случае `name` будет равно `John`, если параметр передан. Если нет, `name` будет равно `null`.

#### 3. Установка значений по умолчанию

Вы можете установить значение по умолчанию для параметра, если он не был передан.

```java
@GetMapping("/students")
public String searchStudents(@RequestParam(defaultValue = "Unknown") String name) {
    // Если name не указан, значение будет "Unknown"
    return "studentList";
}
```

##### Пример URL:

- URL: `http://localhost:8080/students`
- В этом случае `name` будет равно `"Unknown"`.

#### 4. Преобразование типов

`@RequestParam` автоматически преобразует параметры, переданные в строковом формате, в указанные вами типы данных.

```java
@GetMapping("/students")
public String getStudentByAge(@RequestParam int age) {
    // Логика для обработки возраста студента
    return "studentsByAge";
}
```

##### Пример URL:

- URL: `http://localhost:8080/students?age=20`
- В этом случае `age` будет равно `20`.

### Заключение

Аннотация `@RequestParam` в Spring MVC является мощным инструментом для обработки данных, передаваемых через строку запроса. Она обеспечивает разработчикам гибкость в работе с формами и параметрами запроса, позволяя создавать интуитивные интерфейсы для пользователей. Правильное использование этой аннотации способствует более чистому и понятному коду, улучшая обработку входящих HTTP-запросов.