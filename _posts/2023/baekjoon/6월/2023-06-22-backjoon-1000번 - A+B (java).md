---
title: "[BaekJoon] 1000번 - A+B (java)"

categories:
  - BaekJoon

permalink: /baekjoon/1000번 - A+B (java)/

date: 2023-06-22
#last_modified_at: 2021-10-0
---


## 1. 문제
👉 [문제 바로가기](https://www.acmicpc.net/problem/1000)<br><br>
###  - 조건
  
| 시간 제한 | 메모리 제한 |
|:---:|:---:|
|2초|128MB|
  
<br><br>

### - 문제
```두 정수 A와 B를 입력받은 다음, A+B를 출력하는 프로그램을 작성하시오.```
<br><br>

### - 입력
```첫째 줄에 A와 B가 주어진다. (0 < A, B < 10)```
<br><br>

### - 출력
```첫째 줄에 A+B를 출력한다.```
<br><br>

### 예제
  
|입력|출력|
|:---:|:---:|
|1 2|3|
  
<br><br><br>


## 2. 풀이
가장 기초적인 입력 방법인 `Scanner 클래스`를 이용해서 두개의 수를 입력받아 더한 값을 출력하고자 한다.
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
        
        System.out.println(A+B);
        
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

