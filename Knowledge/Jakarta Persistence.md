---
tags:
  - Java
---

> [!NOTE]
> ### Jakarta Persistence
> 
> **Jakarta Persistence**, ранее известная как JPA (Java Persistence API), является спецификацией для управления данными в Java-приложениях с использованием объектов и реляционных баз данных. Она предоставляет набор API для работы с объектно-реляционным отображением (ORM), что позволяет разработчикам работать с базами данных с использованием Java-объектов.

#### Основные концепции Jakarta Persistence

1. **Entity**:
   - Класс, представляющий сущность в базе данных. Он аннотируется с помощью `@Entity` и должен иметь уникальный идентификатор, аннотированный `@Id`.
   
   ```java
   import jakarta.persistence.Entity;
   import jakarta.persistence.Id;

   @Entity
   public class User {
       @Id
       private Long id;
       private String name;

       // Геттеры и сеттеры
   }
   ```

2. **EntityManager**:
   - Основной интерфейс для работы с сущностями. Он отвечает за операции, такие как создание, чтение, обновление и удаление сущностей (CRUD).

   ```java
   import jakarta.persistence.EntityManager;
   import jakarta.persistence.EntityManagerFactory;
   import jakarta.persistence.Persistence;

   public class UserRepository {
       private EntityManagerFactory emf = Persistence.createEntityManagerFactory("my-persistence-unit");

       public void createUser(User user) {
           EntityManager em = emf.createEntityManager();
           em.getTransaction().begin();
           em.persist(user);
           em.getTransaction().commit();
           em.close();
       }
   }
   ```

3. **Persistence Context**:
   - Контекст, в котором управляются сущности. Сущности в пределах одного контекста сохраняют свое состояние между операциями.

4. **JPQL (Java Persistence Query Language)**:
   - Язык запросов, специфичный для JPA, который используется для выполнения запросов к сущностям. Позволяет писать запросы, используя Java-синтаксис.

   ```java
   List<User> users = em.createQuery("SELECT u FROM User u WHERE u.name = :name", User.class)
                        .setParameter("name", "Alice")
                        .getResultList();
   ```

5. **Relationships**:
   - Jakarta Persistence поддерживает отношения между сущностями, такие как "один к одному" (OneToOne), "один ко многим" (OneToMany), "многие ко многим" (ManyToMany). Эти отношения задаются с помощью аннотаций.

   ```java
   import jakarta.persistence.OneToMany;

   @Entity
   public class User {
       @Id
       private Long id;
       private String name;

       @OneToMany(mappedBy = "user")
       private List<Order> orders;
   }
   ```

6. **Lifecycle Callbacks**:
   - Jakarta Persistence позволяет управлять жизненным циклом сущностей с помощью аннотации, такие как `@PrePersist`, `@PostPersist`, `@PreRemove`, которые позволяют выполнять действия до или после операций с сущностями.

#### Преимущества Jakarta Persistence

- **Упрощение работы с базами данных**:
  - Позволяет работать с данными в виде Java-объектов, что уменьшает необходимость в написании SQL-запросов.

- **Интеграция с фреймворками**:
  - Простая интеграция с Java EE и Jakarta EE, что позволяет использовать возможности других технологий, таких как CDI (Contexts and Dependency Injection).

- **Поддержка различных СУБД**:
  - Независимость от конкретной базы данных благодаря использованию ORM и стандартному API.

- **Гибкость в настройках**:
  - Возможность использования различных стратегий кеширования и управления транзакциями.

#### Пример использования Jakarta Persistence

Ниже представлен пример того, как можно использовать Jakarta Persistence для создания и получения сущностей.

```java
import jakarta.persistence.EntityManager;
import jakarta.persistence.EntityManagerFactory;
import jakarta.persistence.Persistence;

public class Main {
    public static void main(String[] args) {
        EntityManagerFactory emf = Persistence.createEntityManagerFactory("my-persistence-unit");
        EntityManager em = emf.createEntityManager();

        // Создание пользователя
        em.getTransaction().begin();
        User user = new User();
        user.setName("Alice");
        em.persist(user);
        em.getTransaction().commit();

        // Получение пользователя
        User foundUser = em.find(User.class, user.getId());
        System.out.println("Найденный пользователь: " + foundUser.getName());

        em.close();
        emf.close();
    }
}
```

#### Заключение

**Jakarta Persistence** — это мощная спецификация для управления данными в Java-приложениях. Она упрощает взаимодействие с реляционными базами данных, позволяет использовать объекты Java для работы с данными и обеспечивает гибкость в управлении системой. Jakarta Persistence является неотъемлемой частью бизнес-приложений, использующих Java EE и Jakarta EE.