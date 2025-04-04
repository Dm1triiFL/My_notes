---
tags:
  - "#Lombok"
---
### Аннотация `@Builder`

**`@Builder`** — это аннотация, предоставляемая библиотекой Lombok в Java, которая автоматически генерирует паттерн Builder для класса. Она позволяет создавать экземпляры классов с множеством параметров, не перегружая конструкторы и улучшая читаемость кода.

#### Основные характеристики `@Builder`

1. **Упрощение создания объектов**:
   - Позволяет создавать объекты с более удобным и читаемым синтаксисом, особенно когда у класса есть много параметров.

2. **Улучшение читаемости**:
   - Код становится более понятным и легким для поддержки, так как параметры и их назначение видно прямо в процессе создания объекта.

3. **Поддержка цепочечных вызовов**:
   - Builder позволяет устанавливать значения параметров в любом порядке, что делает процесс создания объектов менее строгим.

4. **Упрощение работы с неизменяемыми объектами**:
   - Использование `@Builder` часто подходит для создания неизменяемых классов.

### Пример использования `@Builder`

Вот простой пример демонстрации работы аннотации `@Builder` с использованием Lombok.

1. **Добавление зависимости Lombok**:

Если вы используете Maven, добавьте следующую зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.26</version> <!-- Используйте последнюю доступную версию -->
    <scope>provided</scope>
</dependency>
```

2. **Создание класса с использованием `@Builder`**:

```java
import lombok.Builder;
import lombok.Getter;
import lombok.ToString;

@Getter
@Builder
@ToString
public class User {
    private final String username;  // Обязательный параметр
    private final String email;     // Обязательный параметр
    private final String phone;     // Необязательный параметр
}
```

3. **Использование `@Builder` для создания объекта**:

```java
public class Main {
    public static void main(String[] args) {
        User user = User.builder()
                        .username("johndoe")
                        .email("john.doe@example.com")
                        .phone("123-456-7890") // Необязательный параметр
                        .build();

        System.out.println(user);
    }
}
```

### Объяснение примера

1. **Класс `User`**:
   - Содержит параметры, которые могут быть проинициализированы через Builder. Аннотации `@Getter`, `@Builder` и `@ToString` автоматически генерируют геттеры, методы для построения объекта и метод `toString()`, соответственно.

2. **Использование `Builder`**:
   - Метод `User.builder()` создает новый экземпляр Builder, который позволяет устанавливать значения параметров цепочечно. Метод `build()` возвращает экземпляр класса `User`.

### Заключение

Аннотация `@Builder` от Lombok предоставляет мощный инструмент для упрощения процесса создания объектов в Java. Она делает код более читабельным и управляемым, особенно для классов с множеством параметров. Использование `@Builder` позволяет разработчикам экономить время и усилия, тем самым повышая производительность разработки.