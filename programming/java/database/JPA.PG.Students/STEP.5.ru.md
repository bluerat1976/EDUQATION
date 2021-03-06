## Имплементирование на уровне JPA используя Hibernate ORM


### ВТОРАЯ ЧАСТЬ


* Когда вы добавляете параметры подключения к базе данных в **persistence.xml** вы "тюните" поведения драйвера JPA (Hibernate). 

* Если в коде есть такая настройка
    ```xml
    <property name="hibernate.hbm2ddl.auto" value="create" /> 
    ```
  то это говорит о том что при обращении к ДБ через Hibernate, будет задействован инструмент **hbm2ddl** (ddl = Data Definition Language). При значение "create" - Hibernate сам создаст или обновит структуры таблиц - если их нет в базе данных. Простым языком - структура таблиц будет сгенерированна на основании структуры классов и аннотаций сущностей (напр - Student, Group,...)!

  такой режим в продукцию не пускают так как легко можно испортить структуру ДБ. Часто такой подход (когда код приложения генерирует структуру ДБ) - называют **data migration**. Более профессиональные инструменты для мигрирования данных - [liquibase](https://www.liquibase.org/), [flywaydb](https://flywaydb.org/)

* Перед тем как продолжить, убедитесь в том что вы понимаете суть следующих часто используемых аннотаций для сущностей вашего приложения:
 - @Entity
 - @Table(...)
 - @Id
 - @GeneratedValue    
 - @Column(...)    
 - @Size(...)
 - @Min(...)
 - @Max(...)
 - @Max(...)
 - @NotNull
 - @NotBlank
 - @NotEmpy
 ----
 - @OneToOne(...) 
 - @OneToMany(...) 
 - @ManyToOne(...) 
 - @ManyToMany(...) 

дело в том что на основании этих аннотаций, Hibernate "поймет" как правильнее взаимодействуют ваши сущности (объекты) с базой данных а так же между собой.



* Добавим 3 типа сущностей:
  - entities.Student     - класс студента
    с свойствами
    - Long id,           - основной идентификатор / генерируемое значение  
    - String fullname,   - не может быть пустым, минимум 5 символов, макс 30 
    - Date dob,
    - Float mark         - не может быть пустым, минимум 0 максимум 10

    - Group group      - для связи с группой в которой он учится (много - к - одному, так как много студентов в одной группе)

  - entities.Group       - класс группы студентов
    с свойствами
    - Long id,           - основной идентификатор / генерируемое значение  
    - String name,       - не может быть пустым, минимум 2 символа, макс 10

    - Faculty faculty      - для связи с факультетом которому она пренадлежит (много - к - одному, так как много групп в одном факультете)
    - List<Student> students - коллекция студентов в группе ( один - к - многим, так как одна группа относится к многим студентам)

  - entities.Faculty     - класс факультета
    с свойствами
    - Long id,           - основной идентификатор / генерируемое значение  
    - String name,       - не может быть пустым, минимум 2 символа, макс 40

    - List<Group> groups - коллекция групп на данном факультете ( один - к - многим, так как один факультет относится к многим группам)

---

* Добавьте классам и полям необходимые аннотации исходя из изложенного выше

* Дайте знать Hibernate-у о том что у вас есть 3 сущности в **persistence.xml**
  ```xml
  <class>entities.Student</class>
  <class>entities.Group</class>
  <class>entities.Faculty</class>
  ``` 

* Добавьте в Application метод **check()** который всего лишь получит доступ к фабрики менеджеров сущностей и из нее получит менеджера, запустит и закомитит пустую транзакцию! (вызвать метод в main()) при этом база не должна содержать таблицы ло запуска, после запуска Hibernate 3 таблицы с правильной структурой появятся в ДБ university.