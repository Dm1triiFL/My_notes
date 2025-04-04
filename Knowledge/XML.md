---
tags:
  - Term
---

> [!info]
> ## XML (eXtensible Markup Language)
> 
> **XML** (Расширяемый Язык Разметки) — это гибкий формат разметки, который используется для хранения и передачи структурированных данных. XML был разработан с целью облегчить обмен данными между различными системами и людьми. Он является текстовым форматом и поддерживает пользовательские теги, что позволяет описывать данные в понятной форме.

### Основные характеристики XML

1. **Читаемость**: XML-файлы легко читаемы и понимаемы людьми благодаря своему текстовому формату.

2. **Структурированность**: XML позволяет организовывать данные в иерархической структуре с помощью вложенных элементов.

3. **Расширяемость**: Пользователи могут создавать собственные теги и структуры, что делает XML универсальным для различных сценариев.

4. **Платформонезависимость**: XML формат подходит для взаимодействия между разными системами и платформами.

### Структура XML-документа

XML-документ состоит из:
- **Элементов**: Основные строительные блоки XML. Элемент может содержать текст, атрибуты, другие элементы и т.д.
- **Атрибутов**: Дополнительные данные, описывающие свойства элемента, которые добавляются в открывающий тег.
- **Корневого элемента**: Элемент, который содержит все остальные элементы.

#### Пример структуры XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<library>
    <book id="1">
        <title>The Great Gatsby</title>
        <author>F. Scott Fitzgerald</author>
        <year>1925</year>
        <genre>Fiction</genre>
    </book>
    <book id="2">
        <title>1984</title>
        <author>George Orwell</author>
        <year>1949</year>
        <genre>Dystopian</genre>
    </book>
</library>
```

### Основные элементы XML

1. **Корневой элемент**:
   - Каждый XML-документ должен иметь один корневой элемент. В примере выше это элемент `<library>`.

2. **Элементы**:
   - Каждый элемент может содержать текст или другие элементы. Например, элемент `<book>` содержит элементы `<title>`, `<author>`, `<year>` и `<genre>`.

3. **Атрибуты**:
   - Элементы могут иметь атрибуты, которые предоставляют дополнительную информацию. В примере атрибут `id` в элементе `<book>` указывает уникальный идентификатор книги.

### Пример XML-документа

```xml
<?xml version="1.0" encoding="UTF-8"?>
<student>
    <name>John Doe</name>
    <age>21</age>
    <courses>
        <course>Math</course>
        <course>Physics</course>
    </courses>
</student>
```

### Использование XML

XML широко используется в следующих сценариях:

- **Передача данных**: XML используется для обмена данными между различными системами, такими как серверные и клиентские приложения.
- **Хранение данных**: XML может использоваться для хранения конфигурационных данных и других структурированных данных.
- **Веб-сервисы**: XML является основным форматом для SOAP (Simple Object Access Protocol) веб-сервисов.

### Преимущества и недостатки XML

#### Преимущества:
- **Гибкость**: Пользователь может определять собственные теги и структуру.
- **Читаемость**: XML легко читается и воспринимается.
- **Кросс-платформенность**: XML работает на разных уровнях и в разных технологиях.

#### Недостатки:
- **Объем**: XML обычно занимает больше места по сравнению с JSON из-за множественных тегов.
- **Сложность**: Для нового пользователя работа с XML может показаться более сложной из-за необходимости разметки и правил.

### Заключение

XML — это мощный инструмент для представления и хранения данных в структурированном формате. Его гибкость и расширяемость делают его популярным выбором для различных приложений, особенно в сфере обмена данными и взаимодействия между системами. Хотя в последнее время JSON становится более распространенным, XML по-прежнему играет важную роль в веб-разработке и интеграции систем.