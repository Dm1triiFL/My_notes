---
tags:
  - Spring
  - WEB
---

## Модель в Spring MVC

В контексте Spring MVC **модель** (или модель данных) представляет собой уровень, который отвечает за управление данными вашего приложения, включая бизнес-логику, а также взаимодействие с базой данных. Модель может содержать следующие компоненты:

1. **Сущности** (Entities): Классы, которые представляют таблицы в базе данных.
2. **Сервисные классы** (Service classes): Классы, которые содержат бизнес-логику и операции с сущностями.
3. **DAO (Data Access Object)**: Классы, которые отвечают за взаимодействие с базой данных.
4. **Объекты передачи данных ([[DTO]])**: Упрощение структуры данных для передачи по сети или между слоями приложения.

### 1. Сущности (Entities)

Сущности представляют данные в приложении и обычно соответствуют таблицам в базе данных. В Spring MVC они обозначаются с использованием аннотаций JPA.

#### Пример сущности:

```java
import javax.persistence.*;

@Entity
@Table(name = "students")
public class Student {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY) // Автоинкремент
    private Long id;

    private String name;

    // Конструкторы, геттеры и сеттеры
    public Student() {}

    public Student(String name) {
        this.name = name;
    }

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
}
```

### 2. Сервисные классы (Service classes)

Сервисные классы отвечают за бизнес-логику приложения. Они работают с сущностями и содержат методы для выполнения операций, таких как создание, чтение, обновление и удаление данных.

#### Пример сервисного класса:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class StudentService {

    private final StudentRepository studentRepository;

    @Autowired
    public StudentService(StudentRepository studentRepository) {
        this.studentRepository = studentRepository;
    }

    public List<Student> findAll() {
        return studentRepository.findAll();
    }

    public Student findById(Long id) {
        return studentRepository.findById(id).orElseThrow(() -> new StudentNotFoundException("Student not found!"));
    }

    public void addStudent(Student student) {
        studentRepository.save(student);
    }

    // Другие методы по необходимости
}
```

### 3. DAO (Data Access Object)

DAO-слой обычно используется для абстрагирования и инкапсуляции взаимодействия с базой данных. В Spring можно использовать JPA репозитории.

#### Пример DAO с использованием Spring Data JPA:

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface StudentRepository extends JpaRepository<Student, Long> {
    // Методы для работы с сущностями Student могут быть добавлены здесь
}
```

### 4. Объекты передачи данных (DTO)

DTO — это простые объекты, используемые для передачи данных между уровнями приложения, особенно когда вам не нужно передавать всю сущность, а только часть данных.

#### Пример DTO:

```java
public class StudentDTO {
    private Long id;
    private String name;

    // Конструкторы, геттеры и сеттеры
    public StudentDTO(Long id, String name) {
        this.id = id;
        this.name = name;
    }

    public Long getId() {
        return id;
    }

    public String getName() {
        return name;
    }
}
```

### Взаимодействие между контроллером и моделью

Контроллеры используют сервисные классы для извлечения данных из модели и передачи их в представление. Они могут также принимать данные от представления и передавать их сервисам для изменения состояния модели.

#### Пример взаимодействия контроллера с моделью:

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
        model.addAttribute("students", students);
        return "studentList";
    }

    @PostMapping("/add")
    public String addStudent(@RequestParam String name) {
        studentService.addStudent(new Student(name));
        return "redirect:/students";
    }
}
```

### Заключение

**Модель** в Spring MVC представляет собой уровень, отвечающий за данные и бизнес-логику приложения. Она включает сущности, сервисные классы, DAO и DTO. Правильная организация модели и ее взаимодействие с контроллерами обеспечивает эффективное управление данными и бизнес-логикой, что способствует созданию масштабируемых и удобных веб-приложений.