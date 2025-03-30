---
tags:
  - Lombok
---

> [!info]
> ### Аннотация `@Slf4j` (Simple Logging Facade for Java)
> 
> **`@Slf4j`** — это аннотация, предоставляемая библиотекой Lombok в Java, которая автоматически генерирует логгер для класса с использованием библиотеки SLF4J (Simple Logging Facade for Java). Это упрощает работу с логированием, избавляя от необходимости вручную объявлять логгер и определять его настройки для каждого класса.
> 

#### Основные характеристики `@Slf4j`

1. **Автоматическая генерация логгера**:
   - При добавлении аннотации `@Slf4j` в класс, Lombok автоматически создает статическое поле `log` типа `org.slf4j.Logger`.

2. **Упрощение кода**:
   - Позволяет избежать дублирования кода для создания логгера в каждом классе, что улучшает читабельность и поддерживаемость.

3. **Совместимость**:
   - Работает с различными библиотеками логирования, такими как Logback, Log4j и другие, которые поддерживают SLF4J.

### Пример использования `@Slf4j`

Вот простой пример, демонстрирующий использование аннотации `@Slf4j` в классе.

1. **Добавление зависимости Lombok и SLF4J**:

Для Maven, добавьте эти зависимости в ваш `pom.xml`:

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.26</version> <!-- Используйте последнюю доступную версию -->
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-api</artifactId>
    <version>1.7.30</version> <!-- Используйте последнюю доступную версию -->
</dependency>
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-classic</artifactId>
    <version>1.2.3</version> <!-- Используйте последнюю доступную версию -->
</dependency>
```

2. **Создание класса с использованием `@Slf4j`**:

```java
import lombok.extern.slf4j.Slf4j;

@Slf4j
public class UserService {
    
    public void createUser(String username) {
        log.info("Creating user with username: {}", username); // Логирование информации
        // Логика создания пользователя
    }
    
    public void deleteUser(String username) {
        log.warn("Deleting user with username: {}", username); // Логирование предупреждения
        // Логика удаления пользователя
    }
}
```

3. **Использование класса**:

```java
public class Main {
    public static void main(String[] args) {
        UserService userService = new UserService();
        userService.createUser("johndoe");
        userService.deleteUser("johndoe");
    }
}
```

### Объяснение примера

1. **Класс `UserService`**:
   - Использует аннотацию `@Slf4j`, что автоматически создает логгер `log` внутри класса. 

2. **Методы логирования**:
   - В методах `createUser` и `deleteUser` выполняются операции логирования с использованием `log.info` и `log.warn` соответственно. Это позволяет записывать важную информацию о событиях, происходящих в приложении.

### Заключение

Аннотация `@Slf4j` значительно упрощает процесс логирования в приложениях на Java, избавляя разработчиков от ручного определения логгеров для каждого класса. С Lombok и SLF4J вы можете сосредоточиться на бизнес-логике, не отвлекаясь на создание и настройку логгирования, что позволяет улучшить читаемость и поддерживаемость кода.