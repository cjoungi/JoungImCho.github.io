---
title: "[BaekJoon] 15552번 - 빠른 A+B (java)"
#excerpt: "본문의 주요 내용을 여기에 입력하세요"

categories:
  - BaekJoon
tags:
  - [백준, 수학, 구현, 사칙연산]

permalink: /baekjoon/15552번 - 빠른 A+B (java)/


date: 2023-07-21
#last_modified_at: 2022-07-24
---

## 1. 문제
👉 [문제 바로가기](https://www.acmicpc.net/problem/15552)<br><br>
###  - 조건
  
| 시간 제한 | 메모리 제한 |
|:--------:|:--------:|
|1초|512MB|

<br>

### - 문제
```본격적으로 for문 문제를 풀기 전에 주의해야 할 점이 있다. 입출력 방식이 느리면 여러 줄을 입력받거나 출력할 때 시간초과가 날 수 있다는 점이다.```<br>
```C++을 사용하고 있고 cin/cout을 사용하고자 한다면, cin.tie(NULL)과 sync_with_stdio(false)를 둘 다 적용해 주고, endl 대신 개행문자(\n)를 쓰자. 단, 이렇게 하면 더 이상 scanf/printf/puts/getchar/putchar 등 C의 입출력 방식을 사용하면 안 된다.```<br>
```Java를 사용하고 있다면, Scanner와 System.out.println 대신 BufferedReader와 BufferedWriter를 사용할 수 있다. BufferedWriter.flush는 맨 마지막에 한 번만 하면 된다.```<br>
```Python을 사용하고 있다면, input 대신 sys.stdin.readline을 사용할 수 있다. 단, 이때는 맨 끝의 개행문자까지 같이 입력받기 때문에 문자열을 저장하고 싶을 경우 .rstrip()을 추가로 해 주는 것이 좋다.```<br>
```또한 입력과 출력 스트림은 별개이므로, 테스트케이스를 전부 입력받아서 저장한 뒤 전부 출력할 필요는 없다. 테스트케이스를 하나 받은 뒤 하나 출력해도 된다.```

<br><br>

### - 입력
```첫 줄에 테스트케이스의 개수 T가 주어진다. T는 최대 1,000,000이다. 다음 T줄에는 각각 두 정수 A와 B가 주어진다. A와 B는 1 이상, 1,000 이하이다.```

<br><br>

### - 출력
```각 테스트케이스마다 A+B를 한 줄에 하나씩 순서대로 출력한다.```

<br><br>

### - 예제
  
| &nbsp;&nbsp;입력&nbsp;&nbsp; | &nbsp;&nbsp; 출력&nbsp;&nbsp; |
|:--------:|:--------:|
|5<br>1 1<br>12 34<br>5 500<br>40 60<br>1000 1000|2<br>46<br>505<br>100<br>2000|

<br><br><br>


## 2. 풀이
<code><b>반복문 for</b></code>를 사용해 첫 줄에 입력받은 값만큼 A + B를 반복한다.

<div class="border">
for (초기식; 조건식; 증감식) {<br>
 &nbsp;&nbsp;&nbsp;&nbsp;조건식의 결과가 참인 동안 반복적으로 실행하고자 하는 명령문 작성;<br>
}

</div>

<br><br><br>
BufferedReader 입력방식과 2개의 출력방식을 사용해서 결과를 출력한다.
1. <b>BufferedWriter 클래스</b>
2. <b>StringBuilder 클래스</b>
<br><br><br><br>

### - 2. BufferedWriter 클래스 사용
```
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
import java.io.BufferedWriter;
import java.io.OutputStreamWriter;
import java.util.StringTokenizer;

public class Main{
    public static void main(String[] args)throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        
        int num = Integer.parseInt(br.readLine()); 
      
        StringTokenizer st;

        for(int i=0;i<num;i++){
            st = new StringTokenizer(br.readLine()," ");
        
            int a = Integer.parseInt(st.nextToken()); 
            int b = Integer.parseInt(st.nextToken()); 
            bw.write(a+b+"\n");
        }
        br.close();
        bw.flush();
        bw.close();
    }
}
```
> <code><b>Integer.parseInt()</b></code>을 사용해 readLine() 으로 읽어온 String형 데이터를 <code><b>int형으로 변환</b></code>시켜준다.

> <code><b>StringTokenizer</b></code> 를 사용해 한 줄로 읽어온 데이터를 공백을 기준으로 분리하고, <code><b>nextToken()</b></code>을 이용해 순서대로 가져온다.

> BufferedWriter 의 <code><b>flush()</b></code> 를 사용해 모아둔 데이터를 한번에 출력한다.

<br><br>
<b>[여기서 잠깐!]</b>
<div class="box"><code><b>BufferedWriter 클래스</b></code>에 대해 더 알아보고 싶으면 <a href="/java/BufferedReader／BufferedWriter 클래스/"> 여기</a>를 클릭하면 된다.</div>

<br><br><br><br>

### - 2. StringBuilder 클래스 사용
BufferedReader는 `readLine()` 메서드를 사용해 한 행을 전부 읽는다. <br>
이를 **공백단위로 분리**해야 하는데, 두가지 분리 방법으로 문제를 풀어보자.

<br><br>
&nbsp;&nbsp;&nbsp;&nbsp; ① **StringTokenizer** 클래스를 사용하여 분리해주는 방법<br>
&nbsp;&nbsp;&nbsp;&nbsp; ② **split()** 을 사용하는 방법
<br><br><br><br>

#### ① StringTokenizer 클래스를 사용
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
import java.util.StringTokenizer;

public class Main{
    public static void main(String[] args)throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        
        int num = Integer.parseInt(br.readLine()); 
      
        StringTokenizer st;

        for(int i=0;i<num;i++){
            st = new StringTokenizer(br.readLine()," ");
        
            int a = Integer.parseInt(st.nextToken()); 
            int b = Integer.parseInt(st.nextToken()); 
            sb.append(a+b).append("\n");
        }
        br.close();
        System.out.println(sb);
    }
}
```
> <code><b>readLine()</b></code>은 한 줄을 통째로 읽어 String으로 반환하기 때문에 <code><b>StringTokenizer 클래스</b></code>를 사용해 " "(공백)을 기준으로 값을 구분하고, <code><b>nextToken()</b></code>를 사용해 공백으로 구분된 입력값들을 순서대로 가져온다.

> <code><b>Integer.parseInt()</b></code>을 사용해 String형을 <code><b>int형으로 변환</b></code>시켜준다.

> <code><b>StringBuilder 클래스</b></code>는 문자열을 동적으로 조작하기 위한 클래스로, <code><b>append()</b></code> 를 사용해 문자열을 추가하여 새로운 문자열을 생성한다.

> <code><b>sb.append(a+b).append("\n");</b></code>은 불필요한 문자열 연산을 하지 않고 StringBuilder에 직접 추가하기 때문에 <code><b>sb.append(a+b+"\n");</b></code> 보다 더 효율적이고 빠르다.


<br><br><br><br>

#### ② split() 을 사용
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;

public class Main{
    public static void main(String[] args)throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        
        int num = Integer.parseInt(br.readLine()); 
        
        String[] arr;
        
        for(int i=0;i<num;i++){
            arr = br.readLine().split(" "); 
        
            int a = Integer.parseInt(arr[0]); 
            int b = Integer.parseInt(arr[1]); 
            sb.append(a+b).append("\n");
        }
        br.close();
        System.out.println(sb);
    }
}
```
> <code><b>readLine()</b></code>을 통해 한 줄로 받은 String 데이터를 <code><b>split(" ")</b></code> 메서드를 사용해 공백 단위로 나눈 뒤 배열에 저장한다. 

<br><br><br><br>

### - 3. BufferedWriter VS StringBuilder 성능 비교
![image](https://github.com/cjoungi/cjoungi.github.io/assets/113075984/a00d613b-ce85-4f75-b793-245acea2aac0)

출력의 경우 BufferedWriter 보다는 <span class="color"> StringBuilder</span> 가 빠른 것을 볼 수 있다.<br><br>
아무래도 100만개 정도까지는 StringBuilder 가 근소하게 더 빠른 것 같다.<br>
(그러나 데이터 양이 커지면 커질 수록 BufferedWriter 가 더 빠르다.)<br><br>
BufferedWriter는 일반적으로 I/O 작업으로 인해 비교적 느릴 수 있다. 반면에 StringBuilder는 문자열 조작에 최적화된 클래스로, 문자열 연산은 일반적으로 메모리 상에서 수행되므로 상대적으로 빠를 수 있다.
<br><br><br><br>

### - 4. StringTokenizer VS split() 성능 비교
![image](https://github.com/cjoungi/cjoungi.github.io/assets/113075984/71095cf4-5d8e-4520-8956-a3aaabc8cff2)

문자열을 분리할 때, split() 메서드보다 <span class="color">StringTokenizer</span> 가 더 빠르다.

StringTokenizer 클래스는 구분자를 단일 문자로 처리하기 때문에 복잡한 정규식을 사용할 필요가 없다.
그래서 문자열 분리에 대해서는 간단하고 빠른 성능을 보인다.<br><br>

split() 메서드는 정규식을 사용하여 문자열을 분리하기 때문에, 정교한 정규식이 필요하거나 강력한 패턴 매칭이 필요할 때는 사용하는 것이 적절하다. 

<br><br><br>
<span class="color">관련 페이지</span><br>
- [Scanner 클래스](/java/Scanner 클래스/)
- [BufferedReader/BufferedWriter 클래스](/java/BufferedReader／BufferedWriter 클래스/)
<br><br><br>