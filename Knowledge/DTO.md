---
tags:
  - Term
---
## DTO (Data Transfer Object)

**DTO (Data Transfer Object)** — это паттерн проектирования, который используется для передачи данных между процессами. DTO является простым объектом, который не содержит логики бизнеса, а лишь хранит данные. Его основная цель — уменьшить количество вызовов при передаче данных, обеспечивая удобство работы с настройками и интеграцию между различными слоями приложения.

### Основные характеристики DTO

1. **Отделение представления от бизнес-логики**:
   - DTO используются для передачи данных между слоями приложения (например, между контроллерами и сервисами) без включения бизнес-логики.

2. **Упрощение сериализации**:
   - DTO часто используются при обмене данными по сети, например, в REST API, где они могут быть легко сериализованы в форматы, такие как JSON или XML.

3. **Снижение нагрузки**:
   - Передача DTO может уменьшить количество запросов к серверу, особенно когда несколько данных упакованы в один объект.

4. **Кросс-языковая совместимость**:
   - DTO помогает упрощать взаимодействие между различными системами и языками, поскольку они могут быть легко сериализованы и десериализованы.

### Пример использования DTO на Java

Рассмотрим простой пример использования DTO в приложении на Java.

1. **Создание класса DTO**:

```java
public class UserDTO {
    private String username;
    private String email;

    // Конструкторы
    public UserDTO() {}

    public UserDTO(String username, String email) {
        this.username = username;
        this.email = email;
    }

    // Геттеры и сеттеры
    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
```

2. **Использование DTO в контроллере**:

```java
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/users")
public class UserController {
    @PostMapping
    public UserDTO createUser(@RequestBody UserDTO userDTO) {
        // Логика создания пользователя
        // Используем UserDTO для передачи данных
        return userDTO; // Вернем полученный DTO
    }
}
```

### Объяснение примера

1. **Класс `UserDTO`**:
   - Содержит поля (`username`, `email`) с соответствующими геттерами и сеттерами. Он не содержит никакой логики, а только хранит данные.

2. **Контроллер `UserController`**:
   - Принимает объект `UserDTO` в методе `createUser` через JSON-боди запроса. После обработки он может вернуть объект DTO.

### Заключение

**DTO** образуют удобный инструмент для передачи данных между различными слоями и компонентами приложений, особенно в распределенных системах. Использование DTO упрощает сериализацию данных, способствует уменьшению объема передаваемой информации и поддерживает четкое отделение данных от логики бизнеса. Это делает DTO важной частью проектирования современных приложений, особенно тех, которые работают с REST API.