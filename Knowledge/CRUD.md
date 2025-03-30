---
tags:
  - Hibernate
---
## CRUD операции в Hibernate

**CRUD** (Create, Read, Update, Delete) — это основные операции, выполняемые для работы с данными в базе данных. Hibernate предоставляет простые методы для реализации этих операций с объектами, которые моделируют сущности в базе данных.

### 1. Create (Создание)

Создание нового объекта в базе данных осуществляется с помощью метода `save()` сессии. При этом, если объект успешно сохранён, у него автоматически присваивается уникальный идентификатор (ID).

```java
import org.hibernate.Session;
import org.hibernate.Transaction;

public class UserService {

    public void createUser(String username, String password) {
        Session session = HibernateUtil.getSessionFactory().openSession();
        Transaction transaction = null;

        try {
            transaction = session.beginTransaction(); // Начало транзакции

            User user = new User();
            user.setUsername(username);
            user.setPassword(password);

            session.save(user); // Сохранение объекта в базе данных
            transaction.commit(); // Фиксация изменений
        } catch (Exception e) {
            if (transaction != null) {
                transaction.rollback(); // Откат в случае ошибки
            }
            e.printStackTrace();
        } finally {
            session.close(); // Закрытие сессии
        }
    }
}
```

### 2. Read (Чтение)

Чтение данных из базы можно реализовать с помощью методов `get()` и `list()`. Метод `get()` возвращает объект по его идентификатору, тогда как `createQuery()` позволяет выполнять запросы к базе.

#### Получение объекта по ID:

```java
public User getUserById(Long id) {
    Session session = HibernateUtil.getSessionFactory().openSession();
    User user = null;

    try {
        user = session.get(User.class, id); // Получение объекта по ID
    } finally {
        session.close(); // Закрытие сессии
    }
    return user;
}
```

#### Чтение всех пользователей:

```java
import org.hibernate.query.Query;
import java.util.List;

public List<User> getAllUsers() {
    Session session = HibernateUtil.getSessionFactory().openSession();
    List<User> users = null;

    try {
        Query<User> query = session.createQuery("from User", User.class); // JPQL запрос
        users = query.list(); // Получение списка всех пользователей
    } finally {
        session.close(); // Закрытие сессии
    }
    return users;
}
```

### 3. Update (Обновление)

Обновление данных осуществляется с помощью метода `update()`. Получив объект из базы или создав его, вы можете изменить его поля и сохранить изменения.

```java
public void updateUser(Long id, String newUsername, String newPassword) {
    Session session = HibernateUtil.getSessionFactory().openSession();
    Transaction transaction = null;

    try {
        transaction = session.beginTransaction(); // Начало транзакции

        User user = session.get(User.class, id); // Получение объекта по ID
        if (user != null) {
            user.setUsername(newUsername); // Обновление данных
            user.setPassword(newPassword);
            session.update(user); // Сохранение обновленного объекта
        }
        transaction.commit(); // Фиксация изменений
    } catch (Exception e) {
        if (transaction != null) {
            transaction.rollback(); // Откат в случае ошибки
        }
        e.printStackTrace();
    } finally {
        session.close(); // Закрытие сессии
    }
}
```

### 4. Delete (Удаление)

Удаление объекта из базы данных осуществляется с помощью метода `delete()`.

```java
public void deleteUser(Long id) {
    Session session = HibernateUtil.getSessionFactory().openSession();
    Transaction transaction = null;

    try {
        transaction = session.beginTransaction(); // Начало транзакции

        User user = session.get(User.class, id); // Получение объекта по ID
        if (user != null) {
            session.delete(user); // Удаление объекта
        }
        transaction.commit(); // Фиксация изменений
    } catch (Exception e) {
        if (transaction != null) {
            transaction.rollback(); // Откат в случае ошибки
        }
        e.printStackTrace();
    } finally {
        session.close(); // Закрытие сессии
    }
}
```

### Итоговый пример

Вот как все эти операции могут быть объединены в классе `UserService`:

```java
public class UserService {
    // Создание пользователя
    public void createUser(String username, String password) { ... }
    
    // Получение пользователя по ID
    public User getUserById(Long id) { ... }
    
    // Получение всех пользователей
    public List<User> getAllUsers() { ... }
    
    // Обновление пользователя
    public void updateUser(Long id, String newUsername, String newPassword) { ... }
    
    // Удаление пользователя
    public void deleteUser(Long id) { ... }
}
```

### Заключение

CRUD операции — это основа работы с данными в приложениях. Hibernate предоставляет удобные методы для реализации этих операций, минимизируя необходимость в написании SQL-запросов вручную. При использовании Hibernate важно также управлять сессиями и транзакциями для обеспечения целостности данных и правильного функционирования приложений.