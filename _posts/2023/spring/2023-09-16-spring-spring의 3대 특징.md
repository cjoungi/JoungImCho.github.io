---
title: "[Spring] spring의 3대 특징"

categories:
  - Spring
tags:
  - [Spring, DI, IoC, AOP]

permalink: /spring/spring의 3대 특징/


date: 2023-09-16
#last_modified_at: 2022-07-24
---
<br><br>
"토비의 스프링 3.1" 책을 읽으며, 한 문장 한 문장 자세히 공부해 보려고 한다.<br><br>
1장은 **오프젝트와 의존관계**이다.
<br><br><br>

---

## spring의 3대 특징
<br>
spring의 3대 특징은 아래와 같다.<br>

1. 제어의 역전(Inversion of Control) / 의존성 주입(Dependency Injection)
2. 관점 지향 프로그래밍 (Aspect Oriented Programming)
3. 서비스 추상화(PSA : Portable Service Abstraction)

<br><br><br><br>

### 📌 1. 제어의 역전(Inversion of Control) / 의존성 주입(Dependency Injection)
<br>

#### <span class="color">1-1. 제어의 역전이란?</span>
```java
class MemberController {
	private MemberRepository repo = new MemberRepository();
}
```
객체 지향 프로그래밍인 자바에서 클래스는 일반적인 경우 클래스 내에서 필요로 하는 의존성을 **스스로** 만들어 사용했다.<br><br>
위의 예제를 보면 알 수 있듯이, <code>new 연산자</code> 를 통해 객체를 직접 생성하고 의존성을 맺는다.
<br><br><br><br>

그러나 <span class="color">제어의 역전</span>이란 객체의 생성,설정,초기화,소멸 등의 과정을 개발자가 직접 관리하는 것이 아니라,
<u>스프링 프레임워크가 객체의 생명주기를 모두 위임해서 관리</u>하는 것을 의미한다.<br><br><br><br>

스프링 프레임워크에서는 이 역할을 &nbsp;<span class="color">* </span><code>스프링 컨테이너</code>가 해주는데, <u>xml 파일이나 어노테이션 방식</u>으로 스프링 컨테이너에 빈(객체)를 등록하기만 하면 된다.<br><br>


<div style="background-color:#ededed;padding:10px 20px;font-size:.8em"> 
<span style="font-weight:bold;font-size:1em"><span class="color">* </span>스프링 컨테이너란?</span><br><br>
스프링 컨테이너는 스프링 프레임워크의 핵심 부분으로, 빈(Bean)의 생성, 구성 및 관리를 담당한다.<br>
"빈"은 스프링에서 관리하는 객체를 의미하는데, 스프링 컨테이너는 빈의 라이프사이클을 관리한다.<br><br>

스프링 컨테이너의 주요 기능과 구성요소는 다음과 같다.<br>
- <u>빈 팩토리 (Bean Factory)</u>: 빈 팩토리는 빈의 생성과 설정, 재사용, 라이프사이클 관리 등을 담당한다.<br>
- <u>어플리케이션 컨텍스트 (Application Context)</u>: 어플리케이션 컨텍스트는 빈 팩토리를 확장한 것으로, 더 고급 기능을 제공한다.<br>
- <u>스프링 표현 언어 (SpEL, Spring Expression Language)</u>: 스프링 표현 언어는 객체 그래프를 조회하고 조작하는 기능을 제공하는 표현 언어이다.
</div>
<br><br><br><br>

#### <span class="color">1-2. 의존성 주입이란?</span>
의존성 주입은 **제어의 역전의 구체적인 구현 방법** 중 하나로 볼 수 있다.<br><br>

- IoC 원칙을 구현하기 위한 여러 디자인 패턴 중 하나이다.<br>      
- 필요한 객체를 직접 생성하는 것이 아니라, 스프링 컨테이너가 빈으로 등록된 객체를 자동으로 주입시켜 의존성을 맺어주는 행위이다.<br><br><br><br>

##### [Bean 등록 방법]
Bean 을 등록하는 방법에는 2가지가 있다.<br><br>
첫번째는 <code>컴포넌트 스캔</code>을 이용하는 방법. (어노테이션 사용)<br><br>
두번째는 <code>XML 또는 자바의 설정파일</code>을 활용해 직접 등록하는 방법.<br><br><br>

1. **컴포넌트 스캔을 이용하는 방법**<br><br>
아래는 컴포넌트 스캔을 통해 등록가능하며, 일반적으로 가장 많이 사용되는 어노테이션이다.<br><br>
• Component Scanning<br>
&nbsp;&nbsp;&nbsp;• @Component<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;• @Controller<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;• @Service<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;• @Repository<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;• @Configuration<br>
<br><br><br>

2. **Java 설정 파일 방법**<br>
(XML을 사용하는 방법은 Spring Boot 가 나오기 전에 사용하는 방법으로 현재는 많이 사용하지 않으므로 설명은 생략한다.)<br><br>

```java
package org.zerock.controller;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration //설정 관련 애노테이션
public class SampleConfig {
    @Bean // Bean으로 아래 객체 직접등록
    public SampleController sampleController(){
        return new SampleController();
    }
}
```
<br><br><br><br>
##### [의존성 주입의 3가지 방법]
1. <code>필드 주입</code> : 멤버 객체(필드)에 @Autowired 붙이는 방법<br><br>
   - 단점 : 외부에서 변경이 불가능하여 테스트하기 어렵다.<br><br>
```java
@Component
public class SampleService {
@Autowired
private final MemberRepository memberRepository;
}
```
<br><br>
2. <code>Setter 주입(수정자 주입)</code> : setter 메소드 위에 @Autowired 붙이는 방법 (메소드의 파라미로 받는 객체를 BeanFactory에서 가져옴)<br><br>
   - 단점 : setXXX 메서드를 public으로 열어두어야 하기 때문에 언제 어디서든 변경이 가능하다.			     
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;: 객체가 생성될 때 필요한 의존성이 주입되지 않아, 일시적으로 불완전한 상태에 있을 수 있다. 이는 런타임 시에 NullPointerException 등의 예외를 발생시킬 수 있다.<br><br> 
```java
   @Controller
   public class SampleController {

       private SampleService sampleService;

       @Autowired
       public void setSampleService(SampleService sampleService) {
           this.sampleService = sampleService;
       }
   }
```
<br><br>
=> 필드 주입과 수정자 주입은 빈이 생성된 후에 참조를 하기 때문에, <u>의존성 주입 문제가</u> 컴파일 타임에 발견되지 않고 <u>런타임에 발생할 수 있다는 것</u>을 의미한다.
<br><br>따라서 생성자를 통한 주입을 권장!!<br><br><br><br>

3. <code>생성자 주입</code> : 객체가 생성될 때 생성자를 통해 의존성을 주입하는 방법이다. 생성자 주입은 주입받을 의존성을 생성자의 매개변수로 지정함으로써 구현된다.<br><br>
- <u>불변성</u> : 필드를 ‘final’로 선언할 수 있어 오류가 발생할 가능성을 줄여준다. 
- <u>순환 참조 방지</u> : 생성자를 통해 주입하고 실행하면 BeanCurrentlyInCreationException이 발생하게 된다.<br>
  더 나아가서 의존 관계에 내용을 외부로 노출 시킴으로써 어플리케이션을 실행하는 시점에서 오류를 체크할 수 있다.<br>
- <u>테스트 용이</u><br>
- <u>@Autowired 생략 가능</u> : 자바 8 이후, Spring 4.3 버전부터는 생성자가 1개만 존재하고 그 생성자로 주입받을 객체가 빈으로 등록되어 있다면 @Autowired를 생략해도 자동 주입된다.<br><br>


```java
@Service
public class SampleService {
    // Some service methods
}

@Controller
public class SampleController {

    private final SampleService sampleService;

    @Autowired
    public SampleController(SampleService sampleService) {
        this.sampleService = sampleService;
    }
}
```
<br><br><br><br>

##### [의존성 주입을 사용하는 이유? 장점?]
1. 테스트가 용이해진다:<br>
- 단위 테스트 용이: DI를 통해 객체의 의존성을 주입받게 되면, 테스트 시에 실제 객체 대신 모의 객체(mock object)나 스텁(stub)을 주입할 수 있다.
- 테스트 격리: 각각의 컴포넌트나 서비스가 느슨하게 결합되어 있기 때문에, 특정 부분만을 독립적으로 테스트할 수 있다.
<br><br>
2. 코드의 재사용성을 높여준다:<br>
- 모듈화: DI를 사용하면 코드를 모듈화하기 쉬워진다. 특정 기능을 수행하는 코드를 분리하여 다른 프로젝트나 다른 부분에서도 재사용할 수 있다.
- 공통 코드 추출: 공통된 기능을 가진 코드를 별도의 클래스나 메소드로 분리하고, 이를 필요한 곳에서 주입받아 사용함으로써 코드의 중복을 줄이고 재사용성을 높일 수 있다.
<br><br>
3. 객체 간의 의존성(종속성)을 줄이거나 없앨 수 있다:<br>
- 결합도 감소: 객체들이 서로에게 덜 종속적이 되므로, 하나의 변경이 다른 부분에 덜 영향을 미친다.
- 코드 유지 관리 용이: 코드의 의존성이 줄어들면, 특정 코드의 변경이나 유지 관리가 더 쉽게 된다.
<br><br>
4. 객체 간의 결합도를 낮추면서 유연한 코드를 작성할 수 있다:<br>
- 유연한 코드 구조: DI를 사용하면 코드가 더 유연해진다. 이는 객체간의 결합도가 낮아지면 다양한 방식으로 객체를 조합하고 활용할 수 있기 때문이다.
- 확장성: 느슨한 결합은 시스템의 일부분을 쉽게 교체하거나 확장할 수 있도록 해준다.

<br><br><br><br>

#### 1-3. 제어의 역전 / 의존성 주입 정리
<div class="border">
- Spring에서는 제어의 역전을 지원하여, 필요에 따라 개발자대신 스프링 컨테이너가 객체(Bean)들을 제어해준다.<br>
- 스프링 컨테이너는 Bean들의 생명주기(생성 -> 의존성 설정 -> 초기화 -> 소멸)을 관리하며, 필요에 따라 객체 간 의존성 주입을 해준다.<br>
- 제어의 역전은 의존성 주입의 상위 개념이다.<br>
- 의존성 주입 방법 중 생성자 방법이 권장된다.<br>
- 코드의 재사용성을 높이고 테스트가 용이해진다. 객체간의 의존성을 줄이며 유연하고 확장성있는 코드를 작성할 수 있다.<br>
</div><br><br><br><br>

---

### 📌 2. 관점 지향 프로그래밍 (Aspect Oriented Programming)
<br>

#### <span class="color">2-1. 관점 지향 프로그래밍이란?</span>
![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZrxxK%2FbtrxoHWDBA4%2Fhs93YWUYWe1vwIkUr2fru1%2Fimg.png)<br>
<br>객체 지향 프로그래밍(OOP)은 비지니스 로직의 모듈화가 핵심이다.<br>
하지만 OOP의 설계방식으로는 다 해결할 수 없는 단점이 존재하는데 <u>로깅이나 보안 및 트랜잭션 등 공통된 기능들이 흩어져 존재한다는 점이다.</u><br>
이러한 문제를 해결하기 위해 AOP를 사용한다.<br><br>

위의 이미지와 같이 클래스 A, B, C에서 공통적으로 나타나는 색깔 블록은 중복되는 메서드, 필드, 코드 등이다. <br>
이때 예를 들어 클래스 A의 주황색 블록 부분을 수정해야 한다면 클래스 B, C의 주황색 부분도 일일이 찾아 수정해야 한다. 이는 SOLID원칙을 위배하며 유지보수를 어렵게 만든다.<br>
이런 식으로 소스 코드상에서 계속 반복해서 사용되는 부분들을 <code>흩어진 관심사(Crosscutting Concerns)</code>라고 한다. <br><br>

<span class="color">AOP</span>는 서비스 전역에 흩어진 관심사(로깅,트랜잭션,보안 등)를 <code>Aspect로 모듈화</code>하고, 비즈니스 로직으로부터 분리하여 <code>재사용</code>하는 것이다.

<br><br><br><br>

#### <span class="color">2-2. AOP 적용방식</span>
AOP의 적용 방식은 크게 3가지 방법이 있습니다.<br><br>
<code>컴파일 시점</code><br>
- .java 파일을 컴파일러를 통해 .class를 만드는 시점에 부가 기능 로직을 추가하는 방식<br>
- 모든 지점에 적용 가능<br>
- AspectJ가 제공하는 특별한 컴파일러를 사용해야 하기 때문에 특별할 컴파일러가 필요한 점과 복잡하다는 단점<br><br>

<code>클래스 로딩 시점</code><br>
- .class 파일을 JVM 내부의 클래스 로더에 보관하기 전에 조작하여 부가 기능 로직 추가하는 방식<br>
- 모든 지점에 적용 가능<br>
- 특별한 옵션과 클래스 로더 조작기를 지정해야하므로 운영하기 어려움<br><br>

<code>런타임 시점</code><br>
- 스프링이 사용하는 방식<br>
- 컴파일이 끝나고 클래스 로더에 이미 다 올라가 자바가 실행된 다음에 동작하는 런타임 방식<br>
- <u>실제 대상 코드는 그대로 유지되고 프록시 객체를 통해 부가 기능이 적용</u><br>
- 프록시는 메서드 오버라이딩 개념으로 동작하기 때문에 메서드에만 적용 가능 -> 스프링 빈에만 AOP를 적용 가능<br>
- 특별한 컴파일러나, 복잡한 옵션, 클래스 로더 조작기를 사용하지 않아도 스프링만 있으면 AOP를 적용할 수 있기 때문에 스프링 AOP는 런타임 방식을 사용

<br><br><br><br>
#### <span class="color">2-3. AOP 용어</span>
<code>타겟(Target)</code><br>
- <u>핵심 기능을 담고 있는 모듈로</u> 타겟은 부가기능을 부여할 대상이 된다.
<br><br>

<code>어드바이스(Advice)</code><br>
- 어드바이스는 타겟에 제공할 <u>부가기능을 담고 있는 모듈</u>이다.
- Advice 관련 어노테이션
    - @Before : 어드바이스 타겟 메소드가 호출되기 전에 어드바이스 기능을 수행<br>
    - @After : 타겟 메소드의 결과에 관계없이(성공, 예외 상관없이) 타겟 메소드가 완료되면 어드바이스 기능 수행<br>
    - @AfterReturning (정상적 반환 이후) : 타겟 메소드가 성공적으로 결과값을 반환 후에 어드바이스 기능을 수행<br>
    - @AfterThrowing (예외 발생 이후) : 타겟 메소드가 수행 중 예외를 던지게 되면 어드바이스 기능을 수행<br>
    - @Around (메소드 실행 전 후) : 어드바이스가 타겟 메소드를 감싸서 타겟 메소드 호출 전, 후 어드바이스 기능을 수행 -> 스프링 배치의 beforeJob, afterJob과 비슷한 것 같다.
<br><br>

<code>조인포인트(Join Point)</code><br>
- 어드바이스가 적용될 수 있는 위치를 말한다.
- 타겟 객체가 구현한 인터페이스의 모든 메서드는 조인 포인트가 된다.
  <br><br>

<code>포인트 컷(Pointcut)</code><br>
- 어드바이스를 적용할 타겟의 메서드를 선별하는 정규표현식이다.
- 포인트컷 표현식은 execution으로 시작하고 메서드의 Signature를 비교하는 방법을 주로 이용한다.
  <br><br>

<code>애스펙트(Aspect)</code><br>
- 애스펙트는 AOP의 기본 모듈이다.
- 애스펙트 = 어드바이스 + 포인트컷
  <br><br>

<code>프록시 Proxy 객체</code><br>
- 타겟을 감싸서 타겟의 요청을 대신 받아주는 랩핑(Wrapping) 오브젝트
- 클라이언트에서 타겟을 호출하면, 타겟을 감싸고 있는 프록시가 호출되어, 타겟 메소드 실행 전에 선처리, 타겟 메소드 실행 후 후처리를 실행시키도록 구성되어 있다.
- 프록시는 호출을 가로챈 후, 어드바이스에 등록된 기능을 수행 후 타겟 메소드를 호출한다.

<br><br><br><br>

#### <span class="color">2-4. 자주 사용하는 어노테이션</span>
1. @Aspect: 클래스에 이 어노테이션을 붙여 해당 클래스가 Aspect임을 명시한다.
2. @Pointcut: 어떤 메서드가 advice를 받을 것인지를 지정한다.
3. @Before, @After, @Around 등: 어떤 시점에 advice가 실행될 것인지를 지정한다.

```java
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.aspectj.lang.annotation.Pointcut;
import org.springframework.stereotype.Component;

@Aspect
@Component
public class LoggingAspect {

    @Pointcut("execution(* com.example.service.*.*(..))")
    public void serviceMethods() {}

    @Before("serviceMethods()")
    public void logBefore() {
        System.out.println("Method is called");
    }
}

```
<br>
- 이 예제에서 LoggingAspect 클래스는 <code>@Aspect 어노테이션</code>이 붙어 있어 aspect 클래스임을 나타낸다. <br>
- <code>@Pointcut 어노테이션</code>이 지정된 serviceMethods 메서드는 com.example.service 패키지의 모든 메서드에 대한 pointcut을 정의한다. <br>
- <code>@Before 어노테이션</code>이 지정된 logBefore 메서드는 해당 pointcut에서 <u>메서드 호출 전에 실행되는 advice</u>를 정의한다. <br>
- 여기서는 메서드 호출 전에 콘솔에 메시지를 출력한다.

<br><br><br><br>

#### <span class="color">2-5. AOP 특징</span>
1. Spring은 프록시 기반 AOP를 지원한다.
- Spring은 타겟(target) 객체에 대한 프록시를 만들어 제공한다.<br>
- 타겟을 감싸는 프록시는 실행시간(Runtime)에 생성된다.<br>
- 프록시는 어드바이스를 타겟 객체에 적용하면서 생성되는 객체이다.<br>
  <br><br>
2. 프록시(Proxy)가 호출을 가로챈다(Intercept)
- 프록시는 타겟 객체에 대한 호출을 가로챈 다음 어드바이스의 부가기능 로직을 수행하고 난 후에 타겟의 핵심기능 로직을 호출한다.(전처리 어드바이스)<br>
- 또는 타겟의 핵심기능 로직 메서드를 호출한 후에 부가기능(어드바이스)을 수행하는 경우도 있다.(후처리 어드바이스)<br>
  <br><br>
3. Spring AOP는 메서드 조인 포인트만 지원한다.
- Spring은 동적 프록시를 기반으로 AOP를 구현하므로 메서드 조인 포인트만 지원한다.<br>
- 핵심기능(타겟)의 메서드가 호출되는 런타임 시점에만 부가기능(어드바이스)을 적용할 수 있다.<br>
- 반면에 AspectJ 같은 고급 AOP 프레임워크를 사용하면 객체의 생성, 필드값의 조회와 조작, static 메서드 호출 및 초기화 등의 다양한 작업에 부가기능을 적용 할 수 있다.

<br><br><br><br>

---

### 📌 3. 서비스 추상화(PSA : Portable Service Abstraction)
<br>

#### 3-1. <span class="color">서비스 추상화(PSA) 란?</span><br>
<code>어떤 기술을 내부에 숨기고 개발자에게 편의성을 제공해주는 것</code>이 서비스 추상화(Service Abstraction)이다.<br><br>
서비스 추상화를 통해 특정 환경이나 서버, 기술에 종속되지 않으며 유연한 어플리케이션 개발이 가능하다.<br><br>
Spring Web MVC, Spring Transaction, Spring Cache 등이 있다.<br><br><br><br>
spring에서 servlet 기반으로 어플리케이션을 만들고 있음에도 불구하고, servlet 코드는 전혀 보이지 않는다.<br><br>
controller만 봐도 @GetMapping, @PostMapping 등의 어노테이션을 통해 편하게 개발한다. <br><br>
그 기반에는 sevlet 기반으로 코드가 구현되는 것이다.<br><br><br><br>
transaction도 마찬가지이다.<br><br>
원래 JDBC를 사용할 때는 다음과 같이 auto commit 을 꺼야한다.<br><br>
이후 명시적으로 commit 을 호출하면서 transaction 처리를 할 수 있다.
```java
dbConnection.setAutoCommit(false);
~~
dbConnection.commit()
```
<br>
그러나 spring에서는 @Transaction 어노테이션을 메서드에 추가하면 알아서 Transaction 처리가 된다.<br><br>
즉, 내부적으로 복잡함을 감춘 것이다.

<br><br><br><br>

---
참고링크 | <br>
- [[Spring] 의존성 주입, 제어의 역전](https://velog.io/@damiano1027/Spring-%EC%9D%98%EC%A1%B4%EC%84%B1-%EC%A3%BC%EC%9E%85-%EC%A0%9C%EC%96%B4%EC%9D%98-%EC%97%AD%EC%A0%84)
- [의존성 주입 방법](https://ittrue.tistory.com/227)
- [[Spring] 00. Spring Triangle 스프링의 핵심 3대 요소](https://tailerbox.tistory.com/42)
- [의존성 주입 3가지 방법 - (생성자 주입, Field 주입, Setter 주입)](https://dev-coco.tistory.com/70)
- [[Spring] AOP(Aspect Oriented Programming)란? 스프링 AOP란?](https://code-lab1.tistory.com/193)
- [Spring AOP, Aspect 개념 특징, AOP 용어 정리](https://shlee0882.tistory.com/206)
- [Spring - AOP 총정리](https://velog.io/@backtony/Spring-AOP-%EC%B4%9D%EC%A0%95%EB%A6%AC)
<br><br><br>
