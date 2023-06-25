---
title: "[BaekJoon] 1001번(입출력과 사칙연산) - A-B (java)"
#excerpt: "본문의 주요 내용을 여기에 입력하세요"

categories:
  - BaekJoon
tags:
  - [tag1, tag2]

permalink: /baekjoon/1001번(입출력과 사칙연산) - A-B (java)/


date: 2023-06-25
#last_modified_at: 2022-07-24
---

## 1. 문제
👉 [문제 바로가기](https://www.acmicpc.net/problem/1001)<br><br>
###  - 조건
  
| 시간 제한 | 메모리 제한 |
|:--------:|:--------:|
|2초|128MB|

<br>

### - 문제
```두 정수 A와 B를 입력받은 다음, A-B를 출력하는 프로그램을 작성하시오.```
<br><br>

### - 입력
```첫째 줄에 A와 B가 주어진다. (0 < A, B < 10)```
<br><br>

### - 출력
```첫째 줄에 A-B를 출력한다.```
<br><br>

### - 예제
  
| &nbsp;&nbsp;입력&nbsp;&nbsp; | &nbsp;&nbsp; 출력&nbsp;&nbsp; |
|:--------:|:--------:|
|3 2|1|
  
<br><br><br>


## 2. 풀이
가장 기초적인 입력 방법인 `Scanner 클래스`를 이용해서 두개의 수를 입력받아 뺀 값을 출력하고자 한다.
<br>
```java
//Scanner 클래스는 java.util 패키지에 있기 때문에, java.util.Scanner를 import 해준다.
import java.util.Scanner;

public class Main{
    public static void main(String[] args){
        //객체 생성
        Scanner sc = new Scanner(System.in);
        
        //int형 변수 A와 B에 숫자 입력받기
        int A = sc.nextInt();
        int B = sc.nextInt();
        
        System.out.println(A-B);
        
        //사용한 객체 닫기
        sc.close();
    }
}
```
> 위와같이 객체를 생성할 때, Scanner(System.in) 에서 `System.in` 은 입력한 값을 Byte 단위로 읽는 것을 뜻한다.

> **[ sc.close(); 는 꼭 사용해야 할까? ]**<br>
결론부터 말하면 `꼭 닫을 필요는 없다.` <br>
이유는 System.in을 통해 외부로부터
입력을 받을 때 스트림을 이용해 입력을 받는데,<br>
거의 모든 `스트림 인스턴스 사용 후 실제 닫을 필요가 없다`는 공식 사이트 글이 있다.<br>  
resource가 `IO 채널일 때(외부 네트워크, 파일 등)`만 스트림을 닫아주면 된다!!<br>
이런 resource를 사용 중에 다른 곳에서 같은 resource에 접근하여 사용하다보면 코드가 꼬일 수 있다.<br>
그래서 한 입출력에서 resource를 사용했다면, `.close();`를 사용하여 닫아줘야 한다.<br>
아래는 공식 문서에서 가져온 관련 내용이다.<br>

<div style="background-color:#ededed;padding:10px 20px;font-size:.8em">
Streams have a BaseStream.close() method and implement AutoCloseable, but nearly all stream instances do not actually need to be closed after use. Generally, only streams whose source is an IO channel (such as those returned by Files.lines(Path, Charset)) will require closing. Most streams are backed by collections, arrays, or generating functions, which require no special resource management. (If a stream does require closing, it can be declared as a resource in a try-with-resources statement.)
</div>

<br><br><br>