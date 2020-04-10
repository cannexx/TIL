# JPA 프로그래밍 1. 프로젝트 세팅

- JPA의 핵심은 EntityManager

- EntityManager 내부에서 hibernate를 사용하기 때문에 JPA 기반 / hibernate 기반 둘 다 사용가능하다. 

  - [JPA, Hibernate, 그리고 Spring Data JPA의 차이점](https://suhwan.dev/2019/02/24/jpa-vs-hibernate-vs-spring-data-jpa/)

- Spring Data JPA를 사용하면 EntityManager을 직접 사용할 일이 없다.

- spring.jpa.hibernate.ddl-auto
  - db 초기화 전략이다.
  - create : Application이 구동될때마다 새로 스키마를 생성한다.
  - validate : Entity와 Relation과 스키마 정보를 비교해서 일치하지 않으면 Application이 실행되지 않는다.
  - update : Entity가 변경되면, 변경사항을 추가한다. Entity의 멤버변수가 삭제되어도, Relation의 Column은 삭제되지 않으며, Entity의 멤버변수 이름이 변경되어도 Relation의 Column의 이름은 변경되지 않고 새로운 Column이 생성된다.

- Spring Boot에서 hibernate 관련 의존성이 들어오면 HibernateJpaAutoConfiguration에 있는 자동 설정이 진행된다.

  - EntityManager는 자동설정에 의해 EntityManagerFactoryBuilder가 Bean으로 등록되어있기 때문에 Bean으로 주입받아서 사용 가능하다.

- @PersistenceContext를 사용해서 EntityManager를 주입받는다. 

  - @PersistenceContext는 Spring에 비유하면 ApplicationContext 느낌
  - EntityManager를 통해 영속화(Persistence)할 수 있다.
  - EntityManager와 관련된 모든 작업은 한 트랜젝션 안에서 일어나야 한다.
  - Hibernate의 가장 핵심 API는 Session이다.





 



