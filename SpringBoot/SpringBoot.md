SpringBoot
=====================
# 1. Spring과 Spring Boot의 차이

## Spring

- JAVA 언어를 기반으로 다양한 애플리케이션을 개발하기 위한 프로그래밍 틀이다.
- JAVA를 사용한 JSP, Mybatis, JPA 등의 기술들을 더 편리하게 사용할 수 있게 도와주는 프레임워크이다.

## Spring Boot

- Spring 프레임워크 기반의 애플리케이션을 개발할 때 필요한 설정들을 간편하게 설정하여 더 쉽고 빠르게  Spring 애플리케이션을 개발할 수 있게 도와주는 프레임워크이다.

## 1. 설정

### Spring

- spring에서는 XML 설정 파일을 작성하며 웹 설정, 서버 설정,  Bean 객체 등록 및 의존성 주입 등을 개발자가 하나하나 정의해 주어야 한다.

---

**Bean등록**

- xml로 등록하는 법
- java 클래스로 등록하는 법
- 어노테이션을 활용하는법
    - 이 부분은 Spring boot와 뭐가 다를까…
        - Spring boot에서는 @SpringBootAplication에 @ComponentScan 어노테이션이직접 @Component 어노테이션이 붙어있는 클래스를 Bean으로 등록해준다.
        - Spring에서는 xml에서 `<context:component-scan base-package="패키지 경로"/>`형식으로 ComponentScan의 기능을 지정해줄 수 있다..
        - @Configuration파일에 @ComponentScan 어노테이션을 직접 붙여줘서 사용하는 방법도 있다.

---

### Spring Boot

- XML파일을 별도로 설정해줄 필요가 없다. SpringbootApplication에 포함되어 있는 ComponentScan, EnableAutoCongiguration으로 스프링 컨테이너 설정, 빈 등록 등을 자동으로 수행해준다.

## 2. Dependency

### Spring

- 개발자가 직접 dependency들의 버전을 하나하나 맞추어 사용하여야 한다.
만일, 하나의 dependency의 버전을 변경할 시에, 다른 dependency에도 영향을 미친다.
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cb7d1515-18c8-476b-b39f-40fa103ae474/8c684fe8-7d88-43f1-85f4-11c3badc4c4e/Untitled.png)
    

### Spring Boot

- spring-boot-starter(의존성 및 설정 자동화 모듈)를 사용하여 dependency 설정 시 버전 관리를 자동으로 해준다.
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cb7d1515-18c8-476b-b39f-40fa103ae474/13012412-3eb0-4bb9-8897-3060d6b58406/Untitled.png)
    
    확인 시 버전이 자동으로 맞추어져 설정된 것을 볼 수 있다.
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cb7d1515-18c8-476b-b39f-40fa103ae474/4201a551-cacc-4d01-9373-4c6250b7f617/Untitled.png)
    

## 3. 서버

### Spring

- spring은 웹 어플리케이션 배포 시 외부 서버(Tomcat, Jetty)를 사용하여 배포한다.
- 서버에 배포하기 위해 개발자가 직접 별도로 서버 설치 및 설정, 배포를 해야한다.
- war(Web application ARchive) 파일로 압축하여 설치 및 설정했던 tomcat과 같은 was로 배포하여야한다.

### Spring Boot

- spring boot는 내장 서버를 기본적으로 제공하여 개발자가 따로 서버에 대한 설정 및 배포를 하지 않아도 된다.

# 2. Spring Boot에서 Bean이 생성되는 과정

1. SpringBoot 애플리케이션이 실행, spring container 생성
2. @SpringBootApplication에 @ComponentScan 어노테이션이 @Component 어노테이션이 적용되어 있는 클래스들을 스캔.
    
    <aside>
    💡 @Controller, @Service, @Repository 어노테이션은 모두 @Component 어노테이션을 가지고 있다.
    
    </aside>
    
3. 스캔한 클래스들이 Spring container에 Bean객체로 등록할 떄, 의존성 주입이 필요한 객체들의 빈 등록 여부를 판단하여 빈으로 생성되어 있지 않은 객체들은 빈으로 생성한 후 의존성 주입을 해준다.
    1. 필드 주입, 세터 주입 사용한 의존성 주입의 경우에는 해당 필드에 주입 가능한 빈 객체가 존재하지 않을 때 null로 주입되며, 생성자 주입의 경우에는 예외를 던지며 실행이 종료된다. 

<aside>
💡 **Application Context**

Spring Container의 종류 중 하나로 Bean Factory 라는 Spring Container의 기능을 상속받는다. Bean의 등록 및 생성, 조회 등 관리하는 역할을 한다.

</aside>

1. @SpringBootApplication에 @EnableAutoConfiguration 어노테이션이 spring-boot-autoconfigure > META-INF > spring.factories를 읽어 정의되어있는 @Configuration 자바 파일을 Bean으로 추가 등록한다.
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cb7d1515-18c8-476b-b39f-40fa103ae474/e08a41c5-081a-4db9-89b8-5a20f95c77bf/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cb7d1515-18c8-476b-b39f-40fa103ae474/fd072c88-0eba-4d62-aea1-4633bdc74c20/Untitled.png)
    
    1. 의존성 주입이 필요한 객체들 @Autowired가 적용된 생성자나 필드들을 확

# 3. 기본적인 Annotation 정리하기

## Annotation

자바에서 Annotation은 코드 사이에 주석처럼 쓰이며 해당 코드에 특별한 의미 부여, 기능을 수행하도록 해주는 역할을 한다.

### **@ComponentScan**

- @Component, @Configuration, @Controller, @Service, @Repository가 적용된 클래스 Bean들을 찾아 Spring ApplicationContext에 Bean으로 등록을 해준다.

### @Configuration

- Spring 애플리케이션의 설정을 정의하는 클래스를 나타낼 때 사용한다.
- Spring Bean을 정의할 때 사용한다.

### **@Component**

- 개발자가 만든 Class를 Spring Bean객체로 등록할 때 사용한다. ⇒ class 레벨

<aside>
💡 개발자가 직접 작성하여 컨트롤이 **가능**한 클래스에서 사용한다.

</aside>

### **@Bean**

- 개발자가 직접 Bean객체를 정의할 때 사용된다. ⇒ method 레벨

<aside>
💡 개발자가 컨트롤이 **불가능**한 외부 라이브러리 사용 시 사용한다.

</aside>

### @Autowired

- Type에 따라서 Bean을 주입할 때 사용된다.
    
    <aside>
    💡 **@Inject, @Resource 와 비교**
    Bean객체를 **찾는 순서**가 다르다고 한다
    
    @autowired : 타입 → 이름 → @Qualifier
    @Inject : 타입 → @Qualifier→ 이름
    @Resource : 이름 → 타입 → @Qualifier
    
    </aside>
    

### @Qualifier(”{id}”)

- @Autowired와 함께 쓰인다
- 같은 타입의 Bean객체를 발견하면 지정해준 id로 특정 Bean이 주입될 수 있도록 해주는 역할이다.

### @Controller

- Spring MVC 에서 Controller 클래스에 사용된다.
- 주로 **View**를 반환하기 위해 사용한다.
- 데이터를 반환해야하는 경우에는 @RequestBody 어노테이션을 사용해야 한다.

### @RestController

- @Controller에 @RequestBody가 추가된 것이다.
- 주로 **JSON** 형식으로 데이터를 반환하기 위해 사용된다.
- 자동으로 Spring Bean으로 등록된다.

### **@Service**

- **비즈니스 로직**을 수행 하는 Class를 나타내는 용도로 사용된다.

### **@Repository**

- **DB에 접근**하는 메서드를 가진 Class를 나타내는 용도로 사용된다.

### @Mapper

- DB와 객체 간의 매핑을 하는 인터페이스를 정의할 때 사용한다.
- 매퍼임을 표시하는 마커 인터페이스(기능은 없고, 표시를 위한 인터페이스)

### @MapperScan

- basePackages옵션으로 지정한 경로에 존재하는 @Mapper어노테이션으로 명시되어진 인터페이스들을 스캔한다.

### **@RequestMapping**

- 요청 받은 URL을 어떤 메서드에서 처리할지 매핑해주는 역할을 한다.
- Controller에 주로 사용된다.

### @(GET/POST/PUT/DELETE/PATCH)Mapping

- 요청 URL에 대한 각각의 요청(GET/POST/PUT/DELETE/PATCH)을 메소드와 매핑 시켜주는 역할

Todo

@ToString

@Builder

```bash
public class Store {

    private Pencil pencil;

    public Store() {
        this.pencil = new Pencil();
    }

}
```

```bash
public class BeanFactory {
	
Product prod;

@Autowired
    public void store(Product product) {
        // Bean의 생성
        this.product = product
    }
    
}
```
