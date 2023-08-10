---
title: "[BaekJoon] 2742번 - 기찍 N (java)"
#excerpt: "본문의 주요 내용을 여기에 입력하세요"

categories:
  - BaekJoon
tags:
  - [백준, 구현]

permalink: /baekjoon/2742번 - 기찍 N (java)/


date: 2023-07-28
#last_modified_at: 2022-07-24
---

## 1. 문제
👉 [문제 바로가기](https://www.acmicpc.net/problem/2742)<br><br>
###  - 조건
  
| 시간 제한 | 메모리 제한 |
|:--------:|:--------:|
|1초|128MB|

<br>

### - 문제
```자연수 N이 주어졌을 때, N부터 1까지 한 줄에 하나씩 출력하는 프로그램을 작성하시오.```<br>

<br><br>

### - 입력
```첫째 줄에 100,000보다 작거나 같은 자연수 N이 주어진다.```<br>

<br><br>

### - 출력
```첫째 줄부터 N번째 줄 까지 차례대로 출력한다.```
<br><br>

### - 예제
  
| &nbsp;&nbsp;입력&nbsp;&nbsp; | &nbsp;&nbsp; 출력&nbsp;&nbsp; |
|:--------:|:--------:|
|5|5<br>4<br>3<br>2<br>1|

<br><br><br>

---
## 2. 풀이
<br>
### - 알고리즘
<code><b>for 반복문</b></code>을 사용해 첫 줄에 입력받은 값 ~ 1 까지 출력한다.

<div class="border">
for (초기식; 조건식; 증감식) {<br>
 &nbsp;&nbsp;&nbsp;&nbsp;조건식의 결과가 참인 동안 반복적으로 실행하고자 하는 명령문 작성;<br>
}
</div>
<br>
```java
for (int i = N; i >= 1; i--) {
	System.out.println(i);
}
```

<br><br><br><br>
2개의 입력방식을 사용해서 결과를 출력한다.
1. <b>Scanner 클래스</b> 
2. <b>BufferedReader 클래스</b>
<br><br><br><br>

### - 1. Scanner 클래스
```java
import java.util.Scanner;

public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        
        int N = sc.nextInt();
        sc.close();
        
        for(int i = N; i >= 1; i--){
            System.out.println(i);
        }
    }
}
```
> 위와같이 객체를 생성할 때, Scanner(System.in) 에서 <code><b>System.in</b></code> 은 입력한 값을 <code><b>Byte 단위</b></code>로 읽는것을 뜻한다.

> int형 데이터를 입력받기 위해 <code><b>nextInt()</b></code> 메서드를 사용한다.

<br><br>
<b>[여기서 잠깐!]</b>
<div class="box"><b>Scanner</b>에 대해 더 자세히 알고싶다면 <a href="/java/Scanner 클래스/" class="underline"> 여기</a> 를 클릭하세요</div>

<br><br><br>

### - 2. BufferedReader 클래스 사용
3가지 출력 방식으로 문제를 풀어보고 비교해보자.<br>

<br><br>
&nbsp;&nbsp;&nbsp;&nbsp; ① **StringBuilder**<br>
&nbsp;&nbsp;&nbsp;&nbsp; ② **BufferedWriter**<br>
&nbsp;&nbsp;&nbsp;&nbsp; ③ **System.out.println()**<br>

<br><br><br><br>


#### ① BufferedReader + StringBuilder 
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
 
public class Main {
 
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
		int N = Integer.parseInt(br.readLine());
		br.close();
 
		StringBuilder sb = new StringBuilder();
		
		for (int i = N; i >= 1; i--) {
			sb.append(i).append("\n");
		}
		System.out.print(sb);
	}
}
```
> <code><b>Integer.parseInt()</b></code>을 사용해 readLine()으로 읽어온 String형 데이터를 <code><b>int형으로 변환</b></code>시켜준다.

> <code><b>StringBuilder 클래스</b></code>는 문자열을 동적으로 조작하기 위한 클래스로, <code><b>append()</b></code> 를 사용해 문자열을 추가하여 새로운 문자열을 생성한다.

> <code><b>append()</b></code> 를 위와 같이 나눠서 쓰면 타입 변환과 문자열 연결 연산이 추가적으로 발생하지 않고 <u>StringBuilder에 직접 추가하기 때문에</u> 보다 더 효율적이고 빠르다.


<br><br><br><br>

#### ② BufferedReader +  BufferedWriter
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.BufferedWriter;
import java.io.OutputStreamWriter;
import java.io.IOException;

public class Main{
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        
        int N = Integer.parseInt(br.readLine());
        br.close();
        
        for(int i=N;i>=1;i--){
            bw.write(i+"\n");
        }
        bw.flush();
        bw.close();
    }
}
```
> <code><b>BufferedWriter 클래스의 write() 메소드</b></code>는 데이터를 내부 버퍼에 저장하고, <code><b>flush() 메소드</b></code> 를 사용해 버퍼를 비우고 데이터를 출력한다.

> <code><b>BufferedWriter 클래스의 write() 메소드</b></code>는 단독으로 int 형 값만 넣을 경우   아스키 코드값으로 인식되기 때문에 다른 문자가 출력된다. 때문에 <code><b>반드시 문자열과 int 형을 함께 넣어줘야</b></code> int 값을 제대로 출력할 수 있다.

<br><br>
<b>[여기서 잠깐!]</b>
<div class="box"><code><b>BufferedWriter 클래스</b></code>에 대해 더 알아보고 싶으면 <a href="/java/BufferedReader／BufferedWriter 클래스/" class="underline"> 여기</a>를 클릭하면 된다.</div>

<br><br><br><br>


#### ③ BufferedReader + System.out.println()
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;

public class Main{
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        int N = Integer.parseInt(br.readLine());
        br.close();
        
        for(int i=N;i>=1;i--){
            System.out.println(i);
        }
    }
}
```

<br><br><br>

---
## 3. 성능 비교
![image](https://github.com/cjoungi/cjoungi.github.io/assets/113075984/29849c7c-9591-4d23-a385-0189a10c45ed)

위에서 부터 순서대로<br><br>
<b>
BufferedReader + StringBuilder<br>
BufferedReader + BufferedWriter<br>
BufferedReader + System.out.println()<br>
Scanner<br><br>
</b>
위와같이 입력 메소드와 알고리즘 구현 방법에 따라 시간이 달라질 수 있다.<br><br>
<b>입력</b>의 경우 확실히 Scanner 보다는 <span class="color">BufferedReader</span> 가 빠른 것을 볼 수 있다.<br><br>
<b>출력</b>의 경우 System.out.println()와 나머지 간의 차이는 매우 크다.<br>
BufferedWriter 보다는 <span class="color"> StringBuilder</span> 가 빠른 것을 볼 수 있다.<br>
(그러나 데이터 양이 커지면 커질 수록 BufferedWriter 가 더 빠르다.)<br><br>
BufferedWriter는 일반적으로 I/O 작업으로 인해 비교적 느릴 수 있다. <br>
반면에 StringBuilder는 문자열 조작에 최적화된 클래스로, 문자열 연산은 일반적으로 메모리 상에서 수행되므로 상대적으로 빠를 수 있다.

<br><br><br><br>
<span class="color">관련 페이지</span><br>
- [Scanner 클래스](/java/Scanner 클래스/)
- [BufferedReader/BufferedWriter 클래스](/java/BufferedReader／BufferedWriter 클래스/)
<br><br><br>