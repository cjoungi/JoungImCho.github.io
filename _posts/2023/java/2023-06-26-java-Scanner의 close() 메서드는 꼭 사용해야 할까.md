---
title: "[java] Scanner의 close() 메서드는 꼭 사용해야 할까?"
#excerpt: "본문의 주요 내용을 여기에 입력하세요"

categories:
  - Java
tags:
  - [java, Scanner, close, 입출력]

permalink: /java/Scanner의 close() 메서드는 꼭 사용해야 할까/



date: 2023-06-26
#last_modified_at: 2021-10-09
---

## 1. Scanner 객체 사용 후, clone() 메서드를 사용해야 할까?
결론부터 말하면 <span class="color">close() 메서드를 사용하는 것이 좋다!!</span> <br><br>
Scanner는 입력값을 받을 때 사용하는 클래스이다.<br>
자바에서는 모든 입출력, 즉 <code><b>I/O</b></code>가 <span class="color">*</span> <code><b>Stream(스트림)</b></code>을 통해 이루어지는데<br>
사실 아래의 공식문서에 따르면, `'거의 모든 Stream은 굳이 close()를 호출하여 닫을 필요는 없다'` 는 내용이 있다.<br><br>

또한, `Scanner(System.in)` 와 `System.out.println();` 같은 표준 입출력은 프로세스마다 따로 부여되기 때문에
닫지 않아도 문제는 없다. <br>
하지만 혹시 모를 오류와 아래의 예외사항때문에 헷갈리지 않게 `닫아주는 습관`을 갖는 것을 추천한다.

<div style="background-color:#ededed;padding:10px 20px;font-size:.8em">
<span style="font-weight:bold;font-size:1em"><span class="color">* </span>Stream(스트림)이란?</span><br>
여기서 스트림이란 <b>입출력 장치</b>와 <b>자바 프로그램</b>을 연결시켜주는 연결통로이다.<br>
<b>단방향 통신</b>이고 큐의 <b>FIFO</b>(First In First Out) 구조로 되어있다.<br>
예를 들어, 우리가 키보드에 A를 입력한 경우 화면에 A가 출력이 되는데,<br> 키보드에 A가 입력됐음을 듣고 파일에 A를 전송해주는 역할을 스트림이 한다. 
</div>

<br><br>

하지만 `Scanner 객체`를 생성할 때 `System.in` 대신에<br>
<span class="color">I/O 리소스(파일, 네트워크 등)</span>를 사용한다면 `close() 메서드를 명시적으로 호출해야한다!!`<br><br>
공식 문서 [Stream API doc](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html)에서 해당 내용에 대해 언급하고 있다.<br>
<div style="background-color:#ededed;padding:10px 20px;font-size:.8em">
Streams have a BaseStream.close() method and implement AutoCloseable, <b>but nearly all stream instances do not actually need to be closed after use.</b> Generally, <b>only streams whose source is an IO channel (such as those returned by Files.lines(Path, Charset)) will require closing.</b> Most streams are backed by collections, arrays, or generating functions, which require no special resource management. (If a stream does require closing, it can be declared as a resource in a try-with-resources statement.)
</div>
<br>

<br><br><br>

## 2. '왜' close()를 호출해야할까?
리소스를 받아서 사용이 끝나도 해당 리소스는 `자동으로 닫히지 않기 때문이다.`<br>
이런 리소스를 사용 중에 다른 곳에서 같은 리소스에 접근하여 사용하다보면 코드가 꼬일 수 있다.<br>
그래서 사용이 완전히 끝나면 명시적으로 close()를 사용해 `리소스 사용을 중지`하고 `되돌려 줘야 한다.`<br>

<br><br>

---

참고링크 |<br>
[Stream close()에 대해](https://ivvve.github.io/2019/05/23/java/ETC/stream-close/)
<br><br><br>
