---
tags:
  - Spring
---
Инверсия управления (IoC) в контексте [[Spring]] означает, что [[Контейнер Spring]] управляет созданием, жизненным циклом и конфигурацией объектов (или "[[Bean]]"). Ранее разработчик сам создавал и настраивал зависимости внутри своих классов. Используя IoC, вы передаете ответственность за создание объектов и управление их зависимостями контейнеру Spring.

### Основные аспекты IoC в Spring:

1. [**Контейнер бинов**](obsidian://open?vault=IT&file=%D0%9A%D0%BE%D0%BD%D1%82%D0%B5%D0%B9%D0%BD%D0%B5%D1%80%20Spring): Spring управляет объектами через контейнер бинов, который инкапсулирует логику их создания и связывания.
2. **[Внедрение зависимостей](obsidian://open?vault=IT&file=%D0%98%D0%BD%D0%B2%D0%B5%D1%80%D1%81%D0%B8%D1%8F%20%D1%83%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F%20(IoC))**: IoC позволяет внедрять зависимости через:
    - **Конструкторы**: Зависимости передаются в конструктор класса.
    - **Сеттеры**: Зависимости устанавливаются через методы (сеттеры).
    - **Автовнедрение**: Spring автоматически определяет и внедряет зависимости, если они правильно аннотированы.
3. **Конфигурация**: Бины могут настраиваться через XML, Java Config или аннотации.


### Преимущества IoC:

- **Модульность**: Облегчает тестирование, поскольку зависимости можно заменять на заглушки или моки.
- **Снижение связанности**: Компоненты становятся менее зависимыми друг от друга, что упрощает замену и модификацию кода.
- **Управляемое окружение**: Контейнер следит за жизненным циклом объектов, что позволяет избежать утечек памяти и упрощает управление ресурсами.