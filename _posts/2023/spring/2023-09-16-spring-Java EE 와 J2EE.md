---
title: "[Spring] Java EE / J2EE"

categories:
  - Spring
tags:
  - [Spring, 자바]

permalink: /spring/Java EE 와 J2EE/


date: 2023-09-16
#last_modified_at: 2022-07-24
---
<br><br>
"토비의 스프링 3.1" 책을 읽으며, 한 문장 한 문장 자세히 공부해 보려고 한다.<br><br>
1장은 **오프젝트와 의존관계**이다.
<br><br><br>

---
## <span class="color">자바 엔터프라이즈 에디션(Java EE / J2EE)이란?</span>
자바EE는 1999년 썬 마이크로시스템즈가 J2EE(Java 2 Enterprise Edition) 명으로 발표한 <code>분산 애플리케이션 개발 목적의 산업 표준 플랫폼</code>이다.<br><br>
<u>기업용 애플리케이션을 개발/실행하기 위한 기술과 환경을 제공하며</u>, 서블릿(Servlet), JSP, EJB, JDBC, JNDI, JMX, JTA 등의 알려진 기술을 포함하고 있다.<br><br>
자바EE의 주요 목적은 <u>특정 운영체제와 미들웨어에 종속되지 않고 정보 교환 및 애플리케이션 호환</u>이 가능한 플랫폼을 제공하는 것이다.
<br><br><br><br>

## <span class="color">J2EE의 대표 구성 요소</span>
- Servlet : <u>클라이언트가 보내는 HTTP 요청을 처리하는 서버 측 프로그램</u>이며, Servlet 엔진이 있어야 한다.
- JSP(Java Server Pages): <u>HTML 내에 Java 코드를 써서 동적인 웹 페이지를 생성</u>한다. JSP가 처음 실행될 때 Servlet 엔진이 이것을 <u>Servlet으로 컴파일시켜서</u> 내부적으로는 Servlet으로 동작한다.
- EJB(Enterprise Java Beans) : 비즈니스 로직을 처리하는 데 사용되는 <u>서버측 컴포넌트를 쉽게 생성하고 관리할 수 있게 해주는 프레임워크</u>이다.
- Remote Method Invocation(RMI): 프록시를 써서 원격에 있는 Java 객체의 메소드를 실행시키기 위한 기술이다.
- Java Naming DirectoryInterface (JNDI): 자바 기술로 만들어진 객체에 이름을 붙여 찾을 수 있도록 단일한 인터페이스를 제공한다.
- Java Database Connector(JDBC): <u>여러 종류의 데이터베이스 시스템에 접근하는 단일한 인터페이스를 제공</u>한다.<br>
  각각의 데이터베이스에 맞는 <u>JDBC 드라이버</u>가 있어야 한다.
- Java Connector Architecture(JCA): 이기종 플랫폼을 통합할 수 있도록 플랫폼 독립적인 인터페이스를 제공한다.
- Java Message Service (JMS): 여러 가지 메시징 시스템에 대한 플랫폼 독립적인 인터페이스를 제공한다. 
<br><br><br><br>

## <span class="color">초기 Java EE</span>
1장 오브젝트와 의존관계 53p 2번째 줄에 다음과 같이 적혀있다.<br>
<div class="border">
자바 엔터프라이즈 기술의 혼란 속에서 잃어버렸던 객체지향 기술의 진정한 가치를 회복시키고, 그로부터 객체지향 프로그래밍이 제공하는 폭넓은 혜택을 누릴 수 있도록 
기본으로 돌아가자는 것이 바로 스프링의 핵심이다.
</div>
<br><br>

👉 **여기서 말하는 "자바 엔터프라이즈 기술의 혼란"이란 무엇일까?**<br><br>
  <code>초기 자바 엔터프라이즈 에디션</code>(Java EE, 이전에는 J2EE로 알려져 있음)의 <code>복잡성과 낮은 생산성</code>에 대한 비판을 의미한다.<br><br>
  <u>복잡한 XML 구성, 엔터프라이즈 자바빈(EJB) 구성 등 여러 복잡한 설정과 <span class="color">*</span>ceremony 코드</u>를 작성해야 했기 때문에, 객체지향적인 개발보다는 더 <u>절차적인 코드</u>를 작성하게 만들었다.<br><br> 
  이러한 복잡성은 종종 객체 지향 설계 원칙을 적용하는 것을 방해했으며, 코드의 중복, 낮은 유지보수성 등 여러 문제를 일으켰다. <br><br>
  => 스프링 프레임워크가 등장하면서, 이러한 복잡성을 줄이고 개발자들이 객체 지향적인 방식으로 코드를 작성할 수 있게 만드는 방향으로 개선이 이루어졌다.
<br><br>
<div style="background-color:#ededed;padding:10px 20px;font-size:.8em"> 
<span style="font-weight:bold;font-size:1em"><span class="color">* </span>ceremony 코드란?</span><br><br>
개발자들이 실제 기능이나 비즈니스 로직과 관련이 없는 코드나 설정들을 작성해야 하는 상황을 의미한다.<br>
이러한 코드들은 종종 개발 프로세스를 느리게 하며, 코드의 복잡성을 증가시킨다.
</div>

<br><br><br><br>

👉 **여기서 말하는 "잃어버렸던 객체지향 기술의 진정한 가치"란 무엇일까?**<br><br>
  "잃어버렸던 객체지향 기술의 진정한 가치"는 초기의 자바 엔터프라이즈 기술에서 겪었던 복잡성과 과도한 ceremony 코드 작성 등으로 인해 <code>희석되었던 객체지향 프로그래밍의 핵심 원칙과 이점을 찾아가자</code>는 의미이다.<br><br><br>
    [객체지향 프로그래밍의 핵심 원칙 4가지]<br><br>
    - <code>캡슐화(Encapsulation)</code> : 객체의 상태를 외부에서 직접 접근할 수 없도록 숨기고, 상태를 변경할 수 있는 행동만을 외부에 노출시키는 것이다.<br><br>
    - <code>상속(Inheritance)</code> : 기존 클래스의 행동을 확장하거나 변경하기 위해 사용된다.<br><br>
    - <code>다형성(Polymorphism)</code> : 같은 이름의 메서드가 다양한 방식으로 동작하는 것을 가능하게 하며, 이를 통해 코드의 재사용성과 유연성을 향상시킬 수 있다.<br><br>
    - <code>추상화(Abstraction)</code> : 복잡한 내부 구현을 감추고, 객체의 중요한 속성과 행동만을 강조하여 고수준의 개념으로 표현하는 것이다.


<br><br><br><br>

## <span class="color">객체지향프로그래밍이 가능한 언어의 종류</span>
<br>
다음은 대표적인 객체지향 프로그래밍 언어들이다.<br>
- 시뮬라 67(영어: Simula 67) : 최초의 객체 지향 언어
- 스몰토크 : 최초로 GUI를 제공하는 언어
- 비주얼 베이직 닷넷
- 오브젝티브-C : 애플의 운영체제인 iOS에서 사용되는 언어
- C++ : 객체지향성이 더해진 C 언어의 확장형
- C#
- Dart
- 자바
- 객체지향 파스칼
- 델파이
- 파이썬 : 플랫폼 독립적이며 인터프리터식, 객체지향적, 동적 타이핑(dynamically typed) 대화형 언어
- 펄 : 인터프리터 방식의 프로그래밍 언어 혹은 그 인터프리터 소프트웨어
- 루비 : 동적 객체 지향 스크립트 프로그래밍 언어이고, 순수 객체 지향 언어
- 액션스크립트
- ASP
- 스위프트 : 애플이 iOS8 과 OS X 프로그래밍을 위해 개발한 언어
- 참
<br><br><br><br>

이 중 몇개의 언어들만 더 자세히 공부해보자. (+ 이후에 추가 정리)



<br><br><br><br>

---
참고링크 | <br>
- [객체지향언어란? [특징, 장점, 단점, 종류]](https://radait.tistory.com/4)
- [위키백과](https://ko.wikipedia.org/wiki/%EA%B0%9D%EC%B2%B4_%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)
<br><br><br>
