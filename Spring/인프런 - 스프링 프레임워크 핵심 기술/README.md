# [인프런 - 스프링 프레임워크 핵심 기술](https://www.inflearn.com/course/spring-framework_core/dashboard)를 보고 정리한 내용입니다

* [1. IoC 컨테이너 1부 : 스프링 IoC 컨테이너와 빈](#1-IoC-컨테이너-1부--스프링-IoC-컨테이너와-빈)
* [2. IoC 컨테이너 2부 : ApplicationContext와 다양한 빈 설정 방법](#2-IoC-컨테이너-2부--ApplicationContext와-다양한-빈-설정-방법)
* [3. IoC 컨테이너 3부 : @Autowired](#3-IoC-컨테이너-3부--@Autowired)
* [4. IoC 컨테이너 4부 : @Component와 컴포넌트 스캔](#4-IoC-컨테이너-4부--@Component와-컴포넌트-스캔)
* [5. IoC 컨테이너 5부 : Bean Scope](#5-IoC-컨테이너-5부--Bean-Scope)

## 1. IoC 컨테이너 1부 : 스프링 IoC 컨테이너와 빈

### 1-1. Ioc(Inversion of Control)

* IoC란 Inversion of Control의 약자로 의존 관계 주입(Dependency Injection)이라고도 한다.
* IoC는 어떤 객체가 사용하는 ​의존 객체를 직접 만들어 사용하는게 아니라, 어떠한 장치(생성자, Setter 등이 해당)를 통해 주입 받아 사용하는 방법​을 말한다

아래 코드에서 BookService 클래스는 BookRepository 클래스를 의존하는데 이때 new BookRepositiry(); 를 통해 의존 객체를 직접 생성하는 것이 아니라 생성자라는 장치를 통해 의존 객체를 통해 주입받고 있다.

```java
public class BookService {

    private BookRepository bookRepository;

    public BookService(BookRepository bookRepository) {
        this.bookRepositiry=bookRepositiry;
    }
  }
```

> Spring 4.3 이후는 단일 생성자에 한해 묵시적 생성자 주입을 지원한다.

### 1-2. 스프링 IoC 컨테이너

* 스프링 IoC 컨테이너란 IoC 기능을 스프링 프레임워크에 구현한 것이다. 스프링 IoC 컨테이너는 Bean 설정 파일로 부터 Bean 정의를 읽어들이고, Bean을 구성하고 제공하는 역할을 한다.
* 스프링 IoC 컨테이너라 불리는 이유는 IoC 기능을 제공하는 Bean들을 담고 있기 때문에 컨테이너라 불린다.

### 1-3. BeanFactory와 ApplicationContext

* BeanFactory는 스프링 IoC 컨테이너의 핵심 인터페이스로, Bean을 생성하고 관리하는 인터페이스 이다.
* ApplicationContext는 가장 자주 사용하는 인터페이스로 BeanFactory를 상속받으며 메시지 소스 처리 기능(i18n), 이벤트 발행 기능, 리소스 로딩 기능 들이 구현되어 있다.

### 1-4. Bean

스프링 컨테이너가 관리하는 객체를 Bean이라 부르며, Bean의 장점은 아래와 같다.

1. 의존성을 스프링 컨테이너가 관리해 준다.
2. Bean의 기본 Scope는 싱글톤 이기 때문에 런타임시 성능상 이점을 가진다.
3. Bean의 라이프 사이클을 활용하여 추가적인 작업이 가능하다.

## 2. IoC 컨테이너 2부 : ApplicationContext와 다양한 빈 설정 방법

 Spring IoC 컨테이너는 xml 또는 Java로 작성된 Bean 설정 파일을 읽어서 Bean을 스프링 IoC 컨테이너에 등록한다.

![1](./images/1.png)

### 2-1. XML 설정파일

xml을 사용하여 Bean 설정을 정의한 설정파일이며, ApplicationContext를 통해 xml 설정파일을 읽어와서 Spring IoC 컨테이너에 Bean을 등록한다.


bookService와 bookRepository를 Bean으로 등록하며, setter 메소드를 통해 bookService에 있는 bookRepository를 주입 받을수 있도록 설정

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookService" class="com.example.demo.BookService">
        <property name="bookRepository" ref="bookRepository"></property>
    </bean>

    <bean id="bookRepository" class="com.example.demo.BookRepository"></bean>

</beans>
```

ClassPathXmlApplicationContext을 사용하여 application.xml 파일에 있는 Bean 들을 등록한다.

> ClassPathXmlApplicationContext는 클래스패스에 있는 설정파일 위치를 파라미터로 받는다.

```java
@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("application.xml");
        String[] beanDeanDefinitionNames=ctx.getBeanDefinitionNames();
        System.out.println(Arrays.toString(beanDeanDefinitionNames));
    }
}
```

### 2-2. context:component-scan

* 위의 방법인 xml을 사용하여 Bean 설정파일 작성시, 설정 파일이 많아지면 설정 파일을 읽어오는 코드를 계속 추가해 줘야하는 번거로움 존재 한다. 이러한 문제를 해결하기 위해 등장한 방법이 context:component-scan 이다.
* context:component-scan은 스프링 2.5부터 등장하였으며, 지정한 패키지 부터 스캔하여 특정 어노테이션이 등록된 클래스를 Bean으로 등록한다. 특정 어노테이션은 @Component, @Service, @Repository, @Controller, @Configuration 이며, @Service, @Repository, @Controller, @Configuration 어노테이션은 @Component 어노테이션을 확장한 것이다.

com.example.demo 부터 scan을 시작해서 해당 어노테이션이 붙은 클래스를 모두 Bean으로 등록한다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:context=" http://www.springframework.org/schema/context"
           xsi:schemaLocation="http://www.springframework.org/schema/beans">

 <context:component-scan base-package="com.example.demo"></context:component-scan>

</beans>
```

### 2-3. Java Config(자바 설정파일)

xml에 Bean 설정파일을 작성하는 것이 불편함에 따라 등장한 것이 Java 설정파일 이다.

Java 설정파일은 @Configuration을 사용하여 해당 클래스가 Bean 설정파일임을 지정하며, AnnotationConfigApplicationContext 클래스를 통해 Java 설정 파일을 읽어와 스프링 IoC 컨테이너에 등록한다.

```java
@Configuration
public class ApplicationConfig {
    @Bean
    public BookRepository bookRepository() {
        return new BookRepository();
    }

    @Bean
    public BookService bookService() {
        return new BookService();
    }
  }
```

```java
@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        ApplicationContext ctx = new AnnotationConfigApplicationContext("ApplicationConfig.class");
        String[] beanDeanDefinitionNames=ctx.getBeanDefinitionNames();
        System.out.println(Arrays.toString(beanDeanDefinitionNames));
    }
}
```

### 2-4. @ComponentScan

* 위의 Java 설정방법도 xml 처럼 설정파일의 수가 증가시 설정파일들을 등록해줘야 하는 번거로움이 증가한다. 이러한 문제를 해결하기 위해 등장한 방법이 @ComponentScan이다.
* @ComponentScan은 지정한 패키지 또는 지정한 클래스가 위치한 곳 부터 스캔하여 @Component, @Service, @Repository, @Controller, @Configuration 어노테이션이 사용된 클래스를 Bean으로 등록한다.

```java
# basePackages 속성은 패키지를 기준으로 스캔한다.
@ComponentScan(basePackages="com.hong") 

# basePackageClasses 속성은 해당 클래스가 속한 패키지를 기준으로 스캔한다.
@ComponentScan(basePackageClasses=com.hong.SpringInitApplication.class)
```

> Spirng Boot에는 @SpringBootApplication에 @ComponentScan이 적용되어 있다.

## 3. IoC 컨테이너 3부 : @Autowired

스프링 IoC 컨테이너에 담겨있는 Bean의 타입(객체 타입)이 일치하는 것을 찾아서 일치하는 Bean(객체)을 자동으로 주입해주는 어노테이션 이다.

### 3-1. @Autowired를 사용할 수 있는 위치

@Autowired는 생성자, setter, field에서 사용가능 하다.

```java
public class BookService {

    private BookRepository bookRepositiry;

    // 생성자
    @Autowired
    public BookService(BookRepository bookRepositiry) {
        this.bookRepositiry=bookRepositiry;
     }
}
```

```java
public class BookService {

    private BookRepository bookRepositiry;

   // setter
   @Autowired
   public void setBookRepositiry(BookRepository bookRepositiry) {
        this.bookRepositiry = bookRepositiry;
   }
}
```

```java
public class BookService {

    // Field
    @Autowired
    private BookRepository bookRepositiry;
}
```

### 3-2. @Autowired의 required 속성

기본적으로 @Autowired 사용시 스프링 IoC 컨테이너에 해당 타입의 Bean 객체가 존재하지 않거나 또는 해당 타입의 Bean 객체가 2개 이상 존재시 예외를 발생 시키며, 애플리케이션 구동이 실패된다.

만약 위와 같은 경우가 발생해도 예외를 발생시키지 않고 애플리케이션을 구동할려면 @Autowired의 required 속성을 사용하면 된다. required 속성은 Boolean이며 기본값은 true이다. required 속성의 값이 false 일시 해당 Bean을 주입받지 못해도 예외가 발생되지 않고, 애플리케이션은 구동된다.

* 생성자에 @Autowired 사용시 required 속성은 무의미하다. 왜냐하면 생성자는 객체 생성시 필수 요소인데, 필요한 의존성을 주입받지 못하면 객체 생성을 할 수 없기 때문이다.

```java
public class BookService {

    private BookRepository bookRepositiry;

    // 생성자
    @Autowired(required=true)
    public BookService(BookRepository bookRepositiry) {
        this.bookRepositiry=bookRepositiry;
     }
}
```

```java
public class BookService {

    private BookRepository bookRepositiry;

   // setter
   @Autowired(required=false)
   public void setBookRepositiry(BookRepository bookRepositiry) {
        this.bookRepositiry = bookRepositiry;
   }
}
```

```java
public class BookService {

    // Field
    @Autowired(required=false)
    private BookRepository bookRepositiry;
}
```

### 3-3. @Primary와 @Qualifier

@Autowired 사용시 동일한 Type의 bean이 2개일 시 어떤 Bean을 주입받을지 선택해야 하는데, @Primary와 @Qualifier를 사용해서 주입받을 Bean을 지정할 수 있다.

#### 3-3-1. @Primary

@Componet와 @Bean 어노테이션이 사용된 곳에 붙일 수 있는 어노테이션으로, 동일한 타입의 Bean이 2개 이상일시 @Primary가 붙여진 Bean을 주입받는다.

Ioc 컨테이너에 BookRepository 타입의 Bean이 2개 이상일시 @Primary 어노테이션이 붙은 아래 빈을 주입 받는다.

```java
@Component
@Primary
public class BookRepository{}
```

#### 3-3-2. @Qualifier

@Autowired 어노테이션을 통해 의존 주입 받는 대상에 붙이는 어노테이션으로, 동일한 타입의 Bean이 2개 이상일시 Bean 객체 이름이 일치하는 것을 주입 받는다.

Bean의 타입이 BookRepository 이고, Bean의 이름이 BookRepository 인 것을 주입 받는다.

```java
public class BookService{
   @Autowired
   @Qualifier("BookRepository")
   private BookRepository bookRepository;
}
```

## 4. IoC 컨테이너 4부 : @Component와 컴포넌트 스캔

* @ComponentScan 어노테이션은 @Component, @Configuration, @Service, @Repository, @Controller 어노테이션이 사용된 Class를 Bean으로 등록해 주는 역할을 한다.

### 4-1. @ComponentScan

Spring 3.1부터 도입된 어노테이션으로 스프링 3.1부터 도입된 어노테이션으로 지정한 패키지 또는 지정한 클래스가 위치한 곳 부터 스캔하여 @Component, @Configuration, @Service, @Repository, @Controller 어노테이션이 등록된 클래스를 Bean으로 등록한다.

basePackages와 basePackageClasses 속성을 사용해서 스캔 위치를 지정할 수 있다.

#### 4-1-1. basePackages

지정된 패키지부터 스캔한다.

스캔 범위는 com.hong 패키지에 속한 모든 패키지를 스캔한다.

```java
@ComponentScan(basePackages="com.hong")
```

#### 4-1-2. basePackageClasses

해당 클래스가 등록되어 있는 패키지를 스캔하며, class를 사용하기 때문에 문자열을 사용하는 basePackages에 비해 타입 안정성을 보장한다.

```java
@ComponentScan(basePackageClasses=com.hong.SpringInitApplication.class)
```

### 4-2. @Filter

@ComponentScan에서 @Filter 어노테이션을 사용하여 특정 값에 따라 Bean으로 등록하지 않을 수도 있다.

> Filter Type 은 <https://www.baeldung.com/spring-componentscan-filter-type> 참고

```java
@ComponentScan(excludeFilters = {
   @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
   @Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
```

## 5. IoC 컨테이너 5부 : Bean Scope

Bean의 Scope란 Bean 생성 범위를 뜻한다.

### 5-1. Scope의 종류

#### 5-1-1. Singleton

default Scope이며, 인스턴스가 오직 하나만 생성 된다.

#### 5-1-2. Prototype

Bean을 주입받을 때 마다 새로운 인스턴스가 생성 되서 주입받는다.

#### 5-1-3. 그 외

Request, Session, Websocket 이 있다.

### 5-2. Scope 지정하기

Bean을 선언하는 부분에 @Scope 어노테이션을 사용하여 해당 Bean의 Scope를 지정할 수 있다.

```java
@Component
@Scope(value="prototype")
public class prototype{}
```

### 5-3. Prototype Bean이 Singleton Bean을 참조하면?

Singleton은 인스턴스가 오직 하나만 생성되기 때문에 문제가 발생하지 않는다.

### 5-4. Singleton Bean이 Prototype Bean을 참조하면?

Singleton Bean은 ApplicationContext 초기 구동시 인스턴스가 생성되기 때문에 Prototype Bean에 변경사항이 생겨도 해당 변경사항이 업데이트 되지 않는 문제가 발생한다.

이러한 문제는 Prototype Bean을 proxy로 감싸므로써 해결할 수 있다. 아래의 그림처럼 Prototype Bean을 proxy로 감싸는 이유는 Singleton Bean이 Prototype Bean을 직접 참조하면 업데이트 되는 Prototype Bean을 사용할 수 없기 때문이다.

![2](./images/2.png)

Prototype Bean을 proxy로 감싸는 방법은 @Scope의 proxyMode 속성을 사용하는 것이다.

ScopedProxyMode.XXX에서 XXX는 DEFAULT, TARGET_CLASS, INTERFACES, NO가 있다.

* 기본값은 DEFAULT이며, Proxy를 사용하지 않는다는 의미이다.
* TARGET_CLASS는 해당 bean을 클래스 기반 proxy로 감싼다는 의미이다.
* INTERFACES는 해당 bean을 인터페이스 기반 proxy로 감싼다는 의미이다.

```java
@Component 
@Scope(value="prototype", proxyMode=ScopedProxyMode.TARGET_CLASS) 
public class prototype{}
```

### 5-5.  Singleton 객체 사용시 주의할 점

1. Singleton 객체는 인스턴스가 하나만 생성되며 Property가 공유되기 때문에 Property의 값이 보장되지 않는다. 그렇기 때문에 Property 값 변경에 유의해야 한다.
2. ApplicationContext 초기 구동시 인스턴스가 생성되기 때문에 Application 구동시 시간이 걸릴수 있다.