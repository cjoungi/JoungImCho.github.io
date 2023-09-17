---
title: "[Spring] @Async 로 비동기 처리하기"

categories:
  - Spring
tags:
  - [Spring, 비동기]

permalink: /spring/@Async 로 비동기 처리하기/


date: 2023-08-04
#last_modified_at: 2022-07-24
---

## 1. @Async 란?
Spring framework 에서 제공하는 <span class="color">@Async 어노테이션</span> 은 Thread Pool 을 활용하는 <span class="color">비동기 방식의 메서드 실행</span>을 지원한다.<br>
애플리케이션 코어 로직을 수정하지 않고도 <span class="color">*</span> AOP를 통해 메소드를 비동기 처리로 전환할 수 있다.<br>
메서드 호출자는 해당 메서드가 완료될 때까지 기다리지 않고 다음 작업을 진행할 수 있다.<br><br><br>

<div class="box"><span class="color">* AOP</span><br>
AOP(Aspect-Oriented Programming)는 핵심 로직과 부가 기능을 분리하여 애플리케이션 전체에 걸쳐 사용되는 <code><b>부가 기능을 모듈화하여 재사용</b></code>할 수 있도록 지원한다.
Aspect-Oriented Programming이란 단어를 번역하면 <code><b>관점(관심) 지향 프로그래밍</b></code> 이다. 프로젝트 구조를 바라보는 관점을 바꿔보자는 의미이다.
</div>
<br><br><br><br>

---
## 2. ExecutorService 비동기 방식과의 차이

### 2-1. ExecutorService 란?
Java에서 제공하는 <span class="color">ExecutorService</span> 는 Thread Pool 을 관리해주는 유틸리티 클래스이다.<br>
ExecutorService를 사용하여 여러 개의 메서드를 병렬 처리할 수 있다.
<br><br><br><br>

### 2-2. ExecutorService 를 사용한 비동기 방식 구현
```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class Main {
    // 3개의 쓰레드를 가지는 스레드 풀 생성
    ExecutorService executorService = Executors.newFixedThreadPool(3); 

    //Runnable : return 값이 없는 쓰레드
    static Runnable task = new Runnable() {
      public void run() {
        System.out.println("Thread: " + Thread.currentThread().getName());
      }
    };

    public static void main(String[] args) {
        // submit() 은 Callable 또는 Runnable 작업을 쓰레드에 할당
        Future<Void> future = executorService.submit(task);

        try {
            // 작업 처리가 완료되면 null을 리턴
            future.get();
        } catch (Exception e) {
            // Exception Handling
        }

        // ExecutorService를 더 이상 사용하지 않으면 반드시 종료
        executorService.shutdown();
    }
}
```

<br><br><br><br>

### 2-3. ExecutorService 대신 @Async 를 사용하는 이유
- <code><b>간편한 사용</b></code>
  - ExecutorService을 사용하면 비동기 방식의 메소드를 정의 할 때마다, 위와 같이 Runnable의 run()을 재구현해야 하는 등 동일한 작업들을 반복해야 한다.
  - @Async 어노테이션을 사용하면 별도의 ExecutorService를 생성하거나 스레드를 직접 관리할 필요 없이 간편하게 비동기 작업을 수행할 수 있다.

- <code><b>CompletableFuture 사용</b></code>
  - @Async 어노테이션은 기본적으로 CompletableFuture를 사용하여 비동기 작업의 결과를 다루기 때문에 Future 객체를 직접 다루지 않아도 된다.
<br><br><br>

> 일반적으로 <code><b>간단한 비동기 처리</b></code>라면 <code><b>@Async 어노테이션</b></code>을 사용하고, <code><b>커스텀 스레드 풀, 복잡한 비동기 처리</b></code>가 필요한 경우에는 <code><b>ExecutorService</b></code>를 사용하는 것이 좋다.<br>
여기선 간단한 비동기 처리를 위해 @Async 어노테이션을 사용한다.

<br><br><br>

---
## 3. @Async 를 사용한 비동기 메소드 작성
<div class="border">
<code><b>스프링 프레임워크 5 버전 이전</b></code>에서는 만약 커스텀 TaskExecutor 구현체을 따로 생성하지 않았다면, 비동기 작업 처리를 위해 기본적으로 <span class="color">SimpleAsyncTaskExecutor</span> 를 이용해서 스레드를 생성했다.<br>
SimpleAsyncTaskExecutor 는 <code><b>스레드를 재사용하지 않고, 매번 스레드를 새로 만들기 때문에</b></code> @Async를 이용하고 싶다면 ThreadPoolTaskExecutor 으로 설정을 변경해야 했다.
</div>
<div style="text-align:center;font-size:2em">⇩</div>
<div class="border">
<code><b>스프링 프레임워크 5 버전 이후</b></code>부터는 SimpleAsyncTaskExecutor 보다 더 강력한 스레드 풀 기반의 비동기 작업 처리를 위해 <span class="color">ThreadPoolTaskExecutor</span> 가 기본적으로 사용된다. ThreadPoolTaskExecutor는 <code><b>스레드 풀을 사용하여 작업을 처리하므로</b></code> 스레드 생성 비용이 줄어들고, 동시에 실행되는 스레드 수를 제한할 수 있다.
</div>
<br><br><br>

---
## 4. ThreadPoolTaskExecutor
### 4-1. 기본 설정
스레드 풀의 설정을 따로 변경하지 않는다면 ThreadPool의 기본 설정은 아래와 같다.<br><br>
<code><b>corePoolSize (default : 1)</b></code><br>
  - thread-pool에 항상 살아있는 thread의 최소 갯수 
<br><br>

<code><b>maxPoolSize (default : Integer.MAX_VALUE)</b></code><br>
  - thread-pool에서 사용할 수 있는 최대 thread의 갯수 
  - 작업들이 대기열에 가득 쌓여 corePoolSize 개수의 스레드로 처리할 수 없는 상황이 발생하면, 스레드 풀은 maxPoolSize까지 추가 스레드를 생성하여 작업들을 처리
<br><br>

<code><b>queueCapacity (default : Integer.MAX_VALUE)</b></code><br>
  - task가 제출되고 스레드에 의해 수행되기 전 까지 대기하는 queue의 최대 용량
  - corePoolSize의 개수를 넘어서는 task가 들어왔을 경우 queue에 해당 task들이 쌓인다.
<br><br>

<code><b>keepAliveSeconds (default : 60)</b></code><br>
  - 바쁜 작업시간 동안 추가 생성된 스레드들이 한가해지면 idle 한 상태가 되는데,<br>
    corePoolSize를 초과하는 idle 스레드들이 해제되기까지 대기하는 시간 
<br><br>

<code><b>ThreadNamePrefix (default : task-executor-)</b></code><br>
  - thread의 이름의 prefix 
<br><br>

<code><b>allowCoreThreadTimeOut (default : false)</b></code><br>
  - 핵심 스레드(core threads)가 일정 시간 동안 작업이 없을 경우에는 타임아웃을 허용하는지 여부를 나타내는 옵션 

<br><br><br><br>

### 4-2. ThreadPoolExecutor 사용자 설정
- config 설정을 사용해 <code>Bean으로 등록</code><br>
- Application class에 @SpringBootApplication이 있고 스레드 풀을 사용하고자 한다면, 스레드 풀 Config 파일에 @EnableAsync 추가
```java
@Configuration
@EnableAsync
public class AsyncConfig {

	@Bean(name = "executor")
    public ThreadPoolTaskExecutor getAsyncExecutor() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setCorePoolSize(3); // 기본 스레드 수
        executor.setMaxPoolSize(5); // 최대 스레드 수
        executor.setQueueCapacity(10); // 큐 사이즈
        executor.setThreadNamePrefix("async-thread-");
        executor.initialize();
        return executor;
    }
}
```
<br><br><br><br>

### 4-3. ThreadPoolExecutor 동작 원리
- 기본 스레드의 개수가 전부 사용 중이면 사용 가능한 스레드가 나올 때까지 큐에 대기
- 큐에 작업이 꽉차면 최대 스레드 개수만큼 스레드 추가 생성
- 최대 스레드 사용 중이고 큐에 작업이 꽉차면 RejectedExecutionException 발생
- corePoolSize -> queueCapacity -> MaxPoolSize 순으로 동작

<br><br><br><br>

### 4-4. ThreadPoolExecutor 사용
- 스레드 풀을 사용하고자 하는 위치에서 위에서 등록한 Bean을 주입 받아 사용


<br><br><br><br>

---
참고링크 | <br>
- [How does @Async work? @Async를 지금까지 잘 못 쓰고 있었습니다(@Async 사용할 때 주의해야 할 것, 사용법)](https://jeong-pro.tistory.com/187)
- [@Async는 어떤식으로 실행될까?](https://woodcock.tistory.com/31)
- [스프링 @Async와 ThreadPoolTaskExecutor](https://eminentstar.tistory.com/73)
- [[개발자 블로그] ThreadPoolTaskExecutor](https://jeonyoungho.github.io/posts/ThreadPoolTaskExecutor/)
<br><br><br>
