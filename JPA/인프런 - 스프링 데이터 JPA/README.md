> [인프런 - 스프링 데이터 JPA](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EB%8D%B0%EC%9D%B4%ED%84%B0-jpa)를 보고 정리한 내용입니다.

[TOC]

# 1. ORM 개요

ORM은 애플리케이션의 클래스와 SQL 데이터베이스의 테이블 사이의 **맵핑 정보를 기술한 메타데이터**를 사용하여, 자바 애플리케이션의 객체를 SQL 데이터베이스의 테이블에 **자동으로 (또 깨끗하게) 영속화** 해주는 기술입니다.
In a nutshell, object/relational mapping is the automated (and transparent) persistence of objects in a Java application to the tables in an SQL database, using metadata that describes the mapping between the classes of the application and the schema of the SQL database.

> Java Persistence with Hibernate, Second Edition

- 맵핑정보
  - 클래스 - 테이블
  - 필드 - 컬럼

  
# 2. JPA 프로그래밍 1. 프로젝트 세팅

- JPA의 핵심은 EntityManager
- EntityManager 내부에서 hibernate를 사용하기 때문에 JPA 기반 / hibernate 기반 둘 다 사용가능하다. 
- Spring Data JPA를 사용하면 EntityManager을 직접 사용할 일이 없다.
- Spring Boot에서 hibernate 관련 의존성이 들어오면 HibernateJpaAutoConfiguration에 있는 자동 설정이 진행된다.
- EntityManager는 Spring Boot 자동설정에 의해 EntityManagerFactoryBuilder가 Bean으로 등록되어있기 때문에 Bean으로 주입받아서 사용 가능하다.

## 프로젝트 세팅

### application.properties

- DB Connection에 필요한 정보와 DB 초기화 전략 설정

  ```
  spring.datasource.url=jdbc:postgresql://localhost:5432/springdata
  spring.datasource.username=jihun
  spring.datasource.password=pass
  
  spring.jpa.hibernate.ddl-auto=update
  ```

- spring.jpa.hibernate.ddl-auto
  - db 초기화 전략이다.
  - create : Application이 구동될때마다 새로 스키마를 생성한다.
  - validate : Entity와 Relation과 스키마 정보를 비교해서 일치하지 않으면 Application이 실행되지 않는다.
  - update : Entity가 변경되면, 변경사항을 추가한다. Entity의 멤버변수가 삭제되어도, Relation의 Column은 삭제되지 않으며, Entity의 멤버변수 이름이 변경되어도 Relation의 Column의 이름은 변경되지 않고 새로운 Column이 생성된다.

### Account.java

- Entity 클래스이다.

```
@Entity
@Getter
@Setter
public class Account {

    @Id
    @GeneratedValue
    private long id;

    private String username;

    private String password;

}
```

### JpaRunner.java

- Spring Boot 실행시 JPA를 테스트 해보기 위한 클래스이다.
- @PersistenceContext를 사용해서 EntityManager를 주입받는다. 
  - @PersistenceContext는 Spring에 비유하면 ApplicationContext 느낌
  - EntityManager를 통해 영속화(Persistence)할 수 있다.
  - EntityManager와 관련된 모든 작업은 한 트랜젝션 안에서 일어나야 한다.
  - Hibernate의 가장 핵심 API는 Session이다.
- EntityManager 내부에서 hibernate를 사용하기 때문에 JPA 기반 / hibernate 모두 사용해서 영속화를 진행하였다.

```
@Component
@Transactional
public class JpaRunner implements ApplicationRunner {

    @PersistenceContext
    EntityManager entityManager;

    @Override
    public void run(ApplicationArguments args) throws Exception {
        Account account = new Account();
        account.setUsername("jihun");
        account.setPassword("hibernate");

        //hibernate
        Session session = entityManager.unwrap(Session.class);
        session.save(account);

        //jpa
        //entityManager.persist(account);
    }
}
```

## 참고자료

- [JPA, Hibernate, 그리고 Spring Data JPA의 차이점](https://suhwan.dev/2019/02/24/jpa-vs-hibernate-vs-spring-data-jpa/)

# 3. JPA 프로그래밍 : 엔티티 맵핑

Domain 모델을 relation에 어떻게 매핑시킬시 정보를 줘야하는데, 해당 정보를 설정하는 방법은 어노테이션 또는 xml을 사용하는 방법이 존재. 대세는 어노테이션!

## Entity mapping

- @Entity

  - Domain 클래스가 Entity라는 것을 표현
  - Entity는 객체 세상에서 부르는 이름
  - Entity는 자동으로 relation으로 매핑 된다.
  - @Entity에 name 속성을 사용해서 이름을 부여할 수 있다.
    - name 속성은 기본적으로는 클래스의 이름을 사용한다.
    - @Table의 name 속성에 따로 이름을 지정하지 않으면 relation이름은 @Entity의 이름을 따라간다.

  ```
  @Entity
  public class Account {
  
  }
  ```

- @Table

  - relation 세상에서 부르는 이름
  - @Entity의 이름이 기본값이다.
  - 아래 코드에서 relation의 이름은 Account가 아닌 user가 된다.

  ```
  @Entity
  @Table(name = "user")
  public class Account {}
  ```

- @Id

  - Entity의 Primary Key를 mapping 할 때 사용
  - 자바의 모든 primitive type과 wrapper type 모두 사용 가능하다.

  ```
  @Entity
  public class Account {
  
      @Id
      private long id;
  }
  ```

- @GeneratedValue

  - Primary Key의 생성방법을 mapping 하는 어노테이션

  - strategy 속성을 사용해서 생성 전략과 생성기를 설정할 수 있다.

    - 옵션을 정의하지 않을 경우 기본값은 AUTO이며 DB에 따라 생성전략이 달라진다.
    - 생성전략으로 AUTO, TABLE, SEQUENCE, IDENTITY가 있다.

  ```
  @Entity
  public class Account {
  
      @Id
      @GeneratedValue(strategy = GenerationType.AUTO)
      private long id;
      
  }
  ```

- @Column

  - 모든 Entity에 있는 멤버변수에는 @Column이 붙어있다.
  - 다양한 조건이 있다.
    - name, unique, nullable 등....

  ```
  @Entity
  public class Account {
  
  		@Id
      @GeneratedValue(strategy = GenerationType.AUTO)
      private long id;
      
      @Column(name = "user_name", unique = true, nullable = false)
      private String username;
  }
  ```

- @Temporal

  - Column에 날짜 및 시간을 어떻게 저장할지 설정
  - JPA 2.1까지은 Date와 Calendar만 지원
  - JPA 2.2부터 JDK 8에 추가된 LocalDateTime, LocalDate 등 을 지원
    - hibernate 5.3부터 JPA 2.2를 지원한다. - [Hibernate 5.3 release](http://hibernate.org/orm/releases/5.3/)

  ```
  @Entity
  public class Account {
  
      @Id
      @GeneratedValue(strategy = GenerationType.AUTO)
      private long id;
      
      @Temporal(TemporalType.TIMESTAMP)
      private Date createDate = new Date();
  }
  ```

- @Transient

  - 해당 멤버변수를 Column으로 매핑하지 않는다.

```
@Entity
public class Account {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private long id;
    
    @Transient
    private String dummy;
}
```

## 쿼리 출력관련 설정

- spring.jpa.show-sql=true

  - 쿼리 출력

- spring.jpa.properties.hibernate.format_sql=true

  - 쿼리를 보기 좋게 출력

# 4. JPA 프로그래밍 3. Value 타입 맵핑

## Entity 타입이란?

- 고유한 식별자를 가지고 있다. 
  - 예를들어 Primary Key
- 독립적으로 존재하는가
  - 다른 Entity에서 독립적으로 참조 가능한가?

## value 타입이란 ?

- Entity를 통해서 접근가능한 것들
- Value Type 종류
  - primitive Type(String, Date, Boolean, ...) 
  - Composite Value Type
    - primitive Type 보다 조금 더 큰 단위의 Value Type 이다.
  - Collection Value Type

- Composite Value Type
  - primitive Type 보다 조금 더 큰 단위의 Value Type 이다.

  - **Composite Value Type에는 클래스**에 `@Embeddable` 어노테이션을 사용해서 해당 클래스가 Composite Value 임을 지정한다.

  - **Entity 클래스**에서는 `@Embedded` 어노테이션을 사용해서 Composite Value를 사용할 수 있다.

  - Composite Value가 사용된 Entity 클래스에서는 `@AttributeOverrides` 어노테이션과 `@AttributeOverride`을 사용해서 **Composite Value에 정의된 값을 오버라이딩 해서 재정의** 할 수 있다.

## Composite Value Example

### Address.java

- Composite Value 클래스로 `@Embeddable` 가 사용된 것을 알 수 있다.

```
@Embeddable
public class Address {

    private String street;
    private String city;
    private String state;
    private String zipCode;
}

```

### Account.java

- Entity 이다.
- Composite Value에 `@Embedded` 가 사용된 것을 알 수 있다.
- `@AttributeOverrides` 과 ` @AttributeOverride` 를 사용해서 Composite Value에 정의된 값을 오버라이딩 해서 재정의 한 것을 알 수 있다.

```
@Entity
public class Account {

    @Id
    @GeneratedValue()
    private long id;

    @Embedded
    private Address homeAddress;

    @Embedded
    @AttributeOverrides({
            @AttributeOverride(name = "street", column = @Column(name = "company_streat")),
            @AttributeOverride(name = "city", column = @Column(name = "company_city")),
            @AttributeOverride(name = "state", column = @Column(name = "company_state")),
            @AttributeOverride(name = "zipCode", column = @Column(name = "company_zipcode"))
    })
    
    private Address companyAddress;

}

```

# 5. JPA 프로그래밍: 1대다 맵핑

## 관계에는 항상 두 Entity가 존재

- 둘 중 하나는 관계의 주인(owning)이고, 하나는 종속된(non-owning) 쪽이다.
- 관계에서 주인인 쪽은 반대쪽 래퍼런스 쪽을 가지고 있는 쪽이다.
  - 예를들어 Account(Study를 만든사람)와 Study(스터디)와의 관계는?
    - Study를 만든 Account일 경우
      - Study는 하나의 Account를 가질 수 있다.
      - Study에서 Account Reference를 가지고 있기 때문에 Study과 주인이고, Account가 종속된 쪽이다.
    - Account에서 Study를 만들 경우
      - Account는 여러개의 Study를 가질 수 있다.
      - Account에서 Study Reference를 가지고 있기 때문에 Account가 주인이고, Study가 종속된 쪽이다.

## 단방향 Mapping

- @ManyToOne
  - owner에서 non-owning를 하나만 가질 때 사용
    - 예를들어 Study에서 하나의 Account를 가질 때
  - 기본 mapping 방법은 owner에 정의된 non_owning field의 변수이름에 _id를 붙여서 FK를 생성
    - 여기서는 non_owing field의 이름이 owner이기 때문에 owner_id라는 FK가 생성된다.

```
@Entity
@Getter
@Setter
public class Study {

    @Id
    @GeneratedValue
    private Long id;

    private String name;

    @ManyToOne
    private Account owner;

}
```

- @OneToMany
  - owner에서 non-owning를 여러개 가질 때 사용
    - 예를들어 Account에서 여러개의 Study를 가질 때
  - 기본 mapping 방법은 관계에 대한 정보를 가진 Join Table을 생성
    - Join table 이름은 owner Entity 이름_owner Entity에 정의되어 있는 non-owning의 이름
      - 예를들어 Entity의 이름이 Account고 Account에 정의되어 있는 non-owning인 Study의 멤버변수 이름이 studies 일때 Join Table 이름은 account_studies가 된다. 

```
@Entity
@Getter
@Setter
public class Account {

    @Id
    @GeneratedValue
    private long id;

    @OneToMany
    private Set<Study> studies = new HashSet<>();
}
```

> Mapping시 @ManyToOne을 쓸지 @OneToMany를 쓸지 헷갈린다면, 뒤에 One과 Many로 판단! owner에서 non-owning를 하나만 가진다면 One! 이며 여러개를 가지면 Many!

## 양방향 Mapping

만약 Entity가 서로 참조하고 싶을때는 어떻게 해야할까?

- 예를들어 Study에서 Account 정보를 참조하고 싶고 Account에서도 Study 정보를 참조하고 싶을때 아래처럼 작성하면 양방향 관계가 될까?

  - 위의 말대로 아래처럼 코드를 짠다면 양방향 관계가 아닌 2개의 단방향 관계가 되버린다.

  ```
  @Entity
  @Getter
  @Setter
  public class Study {
  
      @Id
      @GeneratedValue
      private Long id;
  
      private String name;
  
      @ManyToOne
      private Account owner;
  
  }
  
  @Entity
  @Getter
  @Setter
  public class Account {
  
      @Id
      @GeneratedValue
      private long id;
  
      @OneToMany
      private Set<Study> studies = new HashSet<>();
  }
  ```

- 양방향 관계로 만들려면 @OneToMany에 mapperBy 속성을 사용해서 이 관계가 owner에 어떻게 mapping이 되어 있는지 관계를 정의한 필드를 명시해 줘야한다.

  - 양방향 Mapping에서는 기본적으로 FK를 가진 쪽이 owner이기 때문에 non-owning인 Account에 mappedBy 속성을 사용해서 owner에 어떻게 mapping 되어있는지 설정해 줬다. 
  - @ManyToOne의 기본 mapping 방법은 owner에 정의된 non_owning field의 변수이름에 _id를 붙여서 FK를 생성

  ```
  @Entity
  @Getter
  @Setter
  public class Study {
  
      @Id
      @GeneratedValue
      private Long id;
  
      private String name;
  
      @ManyToOne
      private Account owner;
  
  }
  
  @Entity
  @Getter
  @Setter
  public class Account {
  
      @Id
      @GeneratedValue
      private long id;
  
  		@OneToMany(mappedBy = "owner")
      private Set<Study> studies = new HashSet<>();
  }
  ```

- 양방향 관계일때는 관계의 주인인 쪽에 관계를 매핑해야한다!!!!!!!

  - 예를들어 아래코드에서 Study가 주인인데 Account에만 관계매핑을 하면 Study에 DB에 관계정보가 정상적으로 설정되지 않는다.

  ```
  @Component
  @Transactional
  public class JpaRunner implements ApplicationRunner {
  
      @PersistenceContext
      EntityManager entityManager;
  
      @Override
      public void run(ApplicationArguments args) throws Exception {
          Account account = new Account();
          account.setUsername("jihun");
          account.setPassword("jpa");
  
          Study study = new Study();
          study.setName("Spring Data JPA");
  
      }
  }
  
  ```

   - 아래처럼 주인인 Study에 관계매핑을 해줘야 DB에 관계정보가 정상적으로 설정된다.


  ```
  @Component
  @Transactional
  public class JpaRunner implements ApplicationRunner {
  
      @PersistenceContext
      EntityManager entityManager;
  
      @Override
      public void run(ApplicationArguments args) throws Exception {
          Account account = new Account();
          account.setUsername("jihun");
          account.setPassword("jpa");
          
          account.getStudies().add(study);
          study.setOwner(account);
  
      }
  }
  ```

- 양방향일때 관계를 설정하는 코드는 보통 convinience method로 묶어서 관계에 한쪽에 넣어서 사용한다.

  - 아래 Account Entity의 addStudy 메서드와 removeStudy 메서드는 양방향 관계를 설정하는 convinience method 이다.

    ```
    @Entity
    @Getter
    @Setter
    public class Account {
    
      @Id
      @GeneratedValue
        private long id;
    
    	@OneToMany(mappedBy = "owner")
        private Set<Study> studies = new HashSet<>();
    
        public void addStudy(Study study){
            this.getStudies().add(study);
        		study.setOwner(this);
        }
    
        public void removeStudy(Study study){
        	this.getStudies().remove(study);
          study.setOwner(null);
        }
    }
    ```

    

















  






