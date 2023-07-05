---
title: "[BaekJoon] 1008번(입출력과 사칙연산) - A/B (java)"
#excerpt: "본문의 주요 내용을 여기에 입력하세요"

categories:
  - BaekJoon
tags:
  - [tag1, tag2]

permalink: /baekjoon/1008번(입출력과 사칙연산) - A/B (java)/


date: 2023-06-26
#last_modified_at: 2022-07-24
---

## 1. 문제
👉 [문제 바로가기](https://www.acmicpc.net/problem/1008)<br><br>
###  - 조건
  
| 시간 제한 | 메모리 제한 |
|:--------:|:--------:|
|2초|128MB|

<br>

### - 문제
```두 정수 A와 B를 입력받은 다음, A/B를 출력하는 프로그램을 작성하시오.```
<br><br>

### - 입력
```첫째 줄에 A와 B가 주어진다. (0 < A, B < 10)```
<br><br>

### - 출력

<code>첫째 줄에 A/B를 출력한다.</code> <br>
<code>실제 정답과 출력값의 절대오차 또는 상대오차가 10<sup>-9</sup> 이하이면 정답이다.</code>
<br><br>

### - 예제
  
| &nbsp;&nbsp;입력&nbsp;&nbsp; | &nbsp;&nbsp; 출력&nbsp;&nbsp; |
|:--------:|:--------:|
|1 3|0.33333333333333333333333333333333|
|4 5|0.8|
  
<br><br><br>


## 2. 풀이
가장 기초적인 입력 방법인 `Scanner 클래스`를 이용해서 두개의 수를 입력받아 나눈 값을 출력하고자 한다.
<br>
```java
//Scanner 클래스는 java.util 패키지에 있기 때문에, java.util.Scanner를 import 해준다.
import java.util.Scanner;

public class Main{
    public static void main(String[] args){
        //객체 생성
        Scanner sc = new Scanner(System.in);
        
        //double형 변수 A와 B에 숫자 입력받기
        double A = sc.nextDouble();
        double B = sc.nextDouble();
        
        //곱한 값 출력하기
        System.out.println(A/B);
        
        //사용한 객체 닫기
        sc.close();
    }
}
```
> 위와같이 객체를 생성할 때, Scanner(System.in) 에서 `System.in` 은 입력한 값을 Byte 단위로 읽는 것을 뜻한다.

<br><br><br>
<span class="color">관련 페이지</span><br>
- [Scanner 클래스](/java/Scanner 클래스/)

- [sc.close()를 꼭 사용해야 할까?](/java/Scanner의 close() 메서드는 꼭 사용해야 할까/)


<br><br><br>