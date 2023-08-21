---
title: "[BaekJoon] 10250번 - ACM 호텔 (java)"
#excerpt: "본문의 주요 내용을 여기에 입력하세요"

categories:
  - BaekJoon
tags:
  - [백준, 수학, 구현, 사칙연산]

permalink: /baekjoon/10250번 - ACM 호텔 (java)/


date: 2023-08-21
#last_modified_at: 2022-07-24
---

## 1. 문제
👉 [문제 바로가기](https://www.acmicpc.net/problem/10250)<br><br>
###  - 조건
  
| 시간 제한 | 메모리 제한 |
|:--------:|:--------:|
|1초|256MB|

<br>

### - 문제
```ACM 호텔 매니저 지우는 손님이 도착하는 대로 빈 방을 배정하고 있다. 고객 설문조사에 따르면 손님들은 호텔 정문으로부터 걸어서 가장 짧은 거리에 있는 방을 선호한다고 한다. 여러분은 지우를 도와 줄 프로그램을 작성하고자 한다. 즉 설문조사 결과 대로 호텔 정문으로부터 걷는 거리가 가장 짧도록 방을 배정하는 프로그램을 작성하고자 한다.```<br>
```문제를 단순화하기 위해서 호텔은 직사각형 모양이라고 가정하자. 각 층에 W 개의 방이 있는 H 층 건물이라고 가정하자 (1 ≤ H, W ≤ 99). 그리고 엘리베이터는 가장 왼쪽에 있다고 가정하자(그림 1 참고). 이런 형태의 호텔을 H × W 형태 호텔이라고 부른다. 호텔 정문은 일층 엘리베이터 바로 앞에 있는데, 정문에서 엘리베이터까지의 거리는 무시한다. 또 모든 인접한 두 방 사이의 거리는 같은 거리(거리 1)라고 가정하고 호텔의 정면 쪽에만 방이 있다고 가정한다.```<br>
<br>
![hotel](https://www.acmicpc.net/upload/images2/elevator.png)<br>

```방 번호는 YXX 나 YYXX 형태인데 여기서 Y 나 YY 는 층 수를 나타내고 XX 는 엘리베이터에서부터 세었을 때의 번호를 나타낸다. 즉, 그림 1 에서 빗금으로 표시한 방은 305 호가 된다.```<br>
```손님은 엘리베이터를 타고 이동하는 거리는 신경 쓰지 않는다. 다만 걷는 거리가 같을 때에는 아래층의 방을 더 선호한다. 예를 들면 102 호 방보다는 301 호 방을 더 선호하는데, 102 호는 거리 2 만큼 걸어야 하지만 301 호는 거리 1 만큼만 걸으면 되기 때문이다. 같은 이유로 102 호보다 2101 호를 더 선호한다.```<br>
```여러분이 작성할 프로그램은 초기에 모든 방이 비어있다고 가정하에 이 정책에 따라 N 번째로 도착한 손님에게 배정될 방 번호를 계산하는 프로그램이다. 첫 번째 손님은 101 호, 두 번째 손님은 201 호 등과 같이 배정한다. 그림 1 의 경우를 예로 들면, H = 6이므로 10 번째 손님은 402 호에 배정해야 한다.```
<br><br>

### - 입력
```프로그램은 표준 입력에서 입력 데이터를 받는다. 프로그램의 입력은 T 개의 테스트 데이터로 이루어져 있는데 T 는 입력의 맨 첫 줄에 주어진다. 각 테스트 데이터는 한 행으로서 H, W, N, 세 정수를 포함하고 있으며 각각 호텔의 층 수, 각 층의 방 수, 몇 번째 손님인지를 나타낸다(1 ≤ H, W ≤ 99, 1 ≤ N ≤ H × W). ```
<br><br>

### - 출력
```프로그램은 표준 출력에 출력한다. 각 테스트 데이터마다 정확히 한 행을 출력하는데, 내용은 N 번째 손님에게 배정되어야 하는 방 번호를 출력한다.```
<br><br>

### - 예제
  
| &nbsp;&nbsp;입력&nbsp;&nbsp; | &nbsp;&nbsp; 출력&nbsp;&nbsp; |
|:--------|:--------|
|2<br>6 12 10<br>30 50 72|402<br>1203|

<br><br><br>

---
## 2. 풀이
2개의 입력방식을 사용해서 결과를 출력한다.
1. <b>Scanner 클래스</b>
2. <b>BufferedReader 클래스</b>
<br><br><br><br>

### 2-0. 알고리즘
방을 배정할 때 우선순위는 다음과 같다.<br>
1. 엘리베이터에서 <u>가까운 거리부터</u> 배정
2. 같은 거리라면 <u>낮은 층수부터</u> 배정<br><br><br>

즉, N번째 손님들의 방배정은 다음과 같다.<br>
![image](https://github.com/cjoungi/cjoungi.github.io/assets/113075984/7d828bb3-255f-4aa7-bf31-f5ffa74397f8)

<br><br><br>
방 번호는 **YXX** 나 **YYXX** 형태이다.<br>
<code>Y</code> 는 층을 의미하고, <code>XX</code> 는 엘리베이터로부터의 거리이다.<br><br>

<span class="color">1. Y 구하기</span> <br>
<code>N에서 H를 나눈 나머지</code> 를 구하면 된다.<br>
N % H 를 계산할 때 가능한 나머지는 **0 ~ 5**이다.<br><br>
예를 들어보자.<br>
H = 6이고 N 이 10이면, <code>10 % 6 = 4</code> 즉, 4층이 된다.
<br><br><br>
**단, 여기서 주의해야 할 점이 있다!**<br>
1 ~ 5층은 가능하지만 ~~0층은 말이 안된다.~~<br> 나머지가 0이 나오는 경우는 N 의 값이 H 의 배수인 경우이다.<br><br>
예를 들어 H = 6 일 때, 6번째, 12번째, 18번째... 손님이 위의 경우인데,<br>
이들은 가장 꼭대기 층수이기 때문에 0이 아닌 <code>H 값이 층수가 된다.</code><br><br>

```java
int Y;

if(N % H == 0){
    Y = H * 100;
}else{
    Y = N % H * 100;
}
```
그런데 방 호수는 YXX 또는 YYXX 으로, 100의 자리수부터 시작하기 때문에 <code>Y * 100</code> 을 하면 된다. 
<br><br><br><br>

<span class="color">2. XX 구하기</span> <br>
<code>N에서 H를 나눈 몫</code> 을 구하고 <code>+ 1</code> 을 하면 된다.<br>
예를 들어, H = 6이고 N 이 10일 때 <code>6 / 10 = 0</code> 이 된다.<br>
무조건 1부터 시작하기 때문에 + 1 을 해줘야 한다.
<br><br><br>
여기서도 주의해야 할 점이 있다!!<br>
N 의 값이 H 의 배수인 경우엔 몫을 구하면 제대로 된 호수가 나온다.<br>
따라서, 이 경우엔 ~~+ 1 을 해 줄 필요가 없다.~~<br><br>

```java
int X;

if(N % H == 0){
    X = N / H;
}else{
    X = N / H + 1;
}
```
<br><br><br><br><br>
이제 Scanner 와 BufferedReader 를 이용해 문제를 풀어보자.

### 2-1. Scanner 클래스
```java
import java.util.Scanner;

public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        
        int T = sc.nextInt(); // 테스트 데이터 수
        
        for(int i=0;i<T;i++){
            int H = sc.nextInt(); // 호텔의 층 수
            int W = sc.nextInt(); // 각 층의 방 수
            int N = sc.nextInt(); // N번째 손님
            
            if(N % H == 0){
                System.out.println(H * 100 + N / H);
            }else{
                System.out.println(N % H * 100 + (N / H + 1));
            }
        }
    }
}
```
> 위와같이 객체를 생성할 때, Scanner(System.in) 에서 <code><b>System.in</b></code> 은 입력한 값을 <code><b>Byte 단위</b></code>로 읽는 것을 뜻한다.

> int형 데이터를 입력받기 위해 <code><b>nextInt()</b></code> 메서드를 사용한다.

<br><br>
<b>[여기서 잠깐!]</b>
<div class="box"><b>Scanner</b>에 대해 더 자세히 알고싶다면 <a href="/java/Scanner 클래스/" class="underline"> 여기</a> 를 클릭하세요</div>

<br><br><br>

### 2-2. BufferedReader 클래스 사용
<br>
문자열 분리 방법으로는 <code>StringTokenizer</code> 클래스를 사용한다.<br>
`readLine()` 메서드를 사용해 읽어온 문자열을 **공백단위로 분리**한다.
<br><br><br>

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
import java.util.StringTokenizer;

public class Main{
    public static void main(String[] args)throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        int T = Integer.parseInt(br.readLine()); // 테스트 데이터 수
        
        for(int i=0;i<T;i++){
            StringTokenizer st = new StringTokenizer(br.readLine());
            
            int H = Integer.parseInt(st.nextToken()); // 호텔의 층 수
            int W = Integer.parseInt(st.nextToken()); // 각 층의 방 수
            int N = Integer.parseInt(st.nextToken()); // N번째 손님
            
            if(N % H == 0){
                System.out.println(H * 100 + N / H);
            }else{
                System.out.println(N % H * 100 + (N / H + 1));
            }
        }
    }
}
```
> <code><b>readLine()</b></code>은 한 줄을 통째로 읽어 String으로 반환하기 때문에, StringTokenizer 클래스의 <code><b>nextToken()</b></code>를 이용해 공백으로 구분된 입력값들을 순서대로 가져온다.

> <code><b>Integer.parseInt()</b></code>을 사용해 String형을 <code><b>int형으로 변환</b></code>시켜준다.

<br><br>
<b>[여기서 잠깐!]</b>
<div class="box"><code><b>BufferedWriter 클래스</b></code>에 대해 더 알아보고 싶으면 <a href="/java/BufferedReader／BufferedWriter 클래스/" class="underline"> 여기</a>를 클릭하면 된다.</div>


<br><br><br>

---
## 3. 성능 비교
![image](https://github.com/cjoungi/cjoungi.github.io/assets/113075984/e3838510-9654-45ae-8d6f-1c023af44ea7)

<b>입력</b>의 경우 확실히 Scanner 보다는 <span class="color">BufferedReader</span> 가 빠른 것을 볼 수 있다.<br><br>

<br><br><br><br>
<span class="color">관련 페이지</span><br>
- [Scanner 클래스](/java/Scanner 클래스/)
- [BufferedReader/BufferedWriter 클래스](/java/BufferedReader／BufferedWriter 클래스/)
<br><br><br>