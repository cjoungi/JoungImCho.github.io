---
title: "[java] BufferedReader/BufferedWriter 클래스"
#excerpt: "본문의 주요 내용을 여기에 입력하세요"

categories:
  - Java
tags:
  - [java, Scanner, 입출력]

permalink: /java/BufferedReader／BufferedWriter 클래스/



date: 2023-06-27
#last_modified_at: 2021-10-09
---

## 1. BufferedReader와 BufferedWriter의 특징
- 입출력 데이터가 바로 전달되지 않고 <span class="color">*</span><code><b>Buffer(버퍼)</b></code>를 거쳐 전달된다.<br>
- 키보드 입력이 있을 때마다 `한 문자씩 버퍼로 전송되고`, <u>버퍼가 가득 차거나 개행문자가 나타나면</u> `버퍼의 내용을 한번에 프로그램에 전달한다.`
- `java.io 패키지`에 존재한다.
- `속도가 빠르다.`<br>
  (흙을 파서 언덕에 버릴 때, 한번 삽질할 때마다 가서 버리는 것보다 수레에 가득 채워서 한번에 나르는 것이 더 효과적인 것과 같은 이치)

<br>
<div class="box">
<span class="color">*</span> <code><b>Buffer</b></code><br>
데이터를 한 곳에서 다른 곳으로 전송하는 동안 일시적으로 그 <code><b>데이터를 보관하는 임시 메모리 영역</b></code>
</div>

<br><br><br>


## 2. BufferedReader 클래스

### - Scanner 클래스와의 차이
1. **Scanner**<br>
- <span style="color:#FF4E02">장점</span><br>
		- `공백문자(' ', '\t', '\n')`를 경계로 하여 입력 값을 인식한다.<br>
		그렇기 때문에 따로 가공할 필요가 없어 편리하다.<br>
		- 또한, `다양한 변수형에 맞는 메서드들`이 있어 원하는 타입의 값을 바로 입력받을 수 있다.
- <span style="color:#FF4E02">단점</span><br> 
		- 버퍼 사이즈가 `1024 char`이기 때문에, 많은 입력을 필요로 할 경우에는 성능상 좋지 못한 결과를 불러온다.
		- 동기화가 되지 않기 때문에 멀티스레드에 안전하지 않다.
<br>
2. **BufferedReader**<br>
- <span style="color:#FF4E02">장점</span><br>
		- Scanner보다 `속도가 빠르다.` 
		- 버퍼 사이즈가 `8192 char(16,384byte)` 이기 때문에, `입력이 많을 때 유리하다.`
		- `동기화`가 되기 때문에 `멀티스레드에 안전하다.`
- <span style="color:#FF4E02">단점</span><br> 
		- `개행문자('\n')`만 경계로 인식한다.<br>
		그래서 입력받은 데이터가 <code><b>String</b></code> 으로 고정되어 있어, 원하는 타입으로 <br>`가공하는 작업이 추가로 필요하다.`<br>
		- <code><b>예외처리</b></code>를 반드시 필요로 한다. <br>
		readLine()시 마다 `try/catch문`으로 감싸주거나, `throws IOException` 을 통한 예외처리를 해도 된다.(대부분의 경우에 후자를 사용)

<br>
> `Scanner`에 대해 더 자세히 알고싶다면 [여기](/java/Scanner 클래스/)를 눌러보자

<br><br><br>

### - BufferedReader 사용법
```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
```
- BufferedReader는 객체를 생성할 때, <span class="color">*</span> `InputStreamReader 객체`를 `생성자의 인자`로 전달한다.<br>
- BufferedReader를 통해 읽어온 데이터는 `개행문자 단위(Line 단위)`로 나누어진다. <br>
- 만약 이를 공백 단위로 데이터를 가공하고자 하면 따로 작업을 해주어야 한다.<br>
이때 사용하는 것이 <span class="color">* StringTokenizer</span> 클래스나 <span class="color"> * String.split()</span> 메서드다.<br><br>

<div class="box">
<span class="color">*</span> <b>InputStreamReader</b><br>
InputStreamReader 클래스는 바이트 단위 데이터를 <b>문자 단위</b> 데이터로 처리할 수 있도록 변환해준다. <br>
그래서 inputStream으로는 읽지 못하는 3byte 의 <b>한글을 읽을 수 있고,</b> <b>char 배열</b>로 데이터를 받을 수 있다.<br><br>
그러나 우리가 문자열을 입력하고 싶다면 매번 배열을 선언해야 한다는 단점이 있다.<br>
이 때, 함께 쓰는 것이 <b>BufferedReader</b>이다.<br>
BufferedReader를 사용해서 <b>Buffer(버퍼)</b>에 입력받은 문자를 쌓아둔 뒤 <b>한번에 문자열처럼 보낸다.</b>
</div>


<div class="box">
<span class="color">*</span> <b>StringTokenizer</b><br>
StringTokenizer 클래스는 우리가 지정한 <b>구분자로 문자열을 쪼개주는 클래스</b>입니다. <br>
그렇게 쪼개어진 문자열을 우리는 <b>토큰(token)</b>이라고 부릅니다.
</div>


<div class="box">
<span class="color">*</span> <b>String.split()</b><br>
String 클래스의 split() 메서드는 <b>구분자를 기준으로 문자열을 쪼개어 배열에 담아 저장</b>하는 함수이다.<br>
split(" ")처럼 인수에 공백과 같은 구분자를 넣어주면 된다.
</div>

<br><br><br>

아래의 예제를 보자

```java
//java.io 패키지에 있는 (BufferedReader, InputStreamReader, IOException) import 필수
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
//java.util 패키지에 있는 StringTokenizer import 필수
import java.util.StringTokenizer;

public class Main{
					   //예외처리가 반드시 필요!!
    public static void main(String[] args) throws IOException{

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        //readLine() 메서드를 사용해서 String형 변수에 입력값 저장
        String str = br.readLine();

	//1. StringTokenizer
	StringTokenizer st = new StringTokenizer(str);
	//공백문자가 나오기 전까지의 입력값을 A에 저장
	int A = Integer.parseInt(st.nextToken());
	//두번째 공백문자가 나오기 전까지의 입력값을 B에 저장
	int B = Integer.parseInt(st.nextToken());

	//2. String.split()
	//문자열을 공백단위로 끊어 배열에 저장
	String arr[] = str.split(" ");
    }
}
```
> 아래의 코드를 자세히 알아보자.<br>
> <div class="color" style="font-size:.85em">BufferedReader br = new BufferedReader(new InputStreamReader(System.in));</div>
1．<code><b>in</b></code>이 `byte 타입`으로 입력값을 읽어들인다.<br>
2．<code><b>InputStreamReader</b></code>가 1번의 값을 `char 타입`으로 변환한다.<br>
3．<code><b>BufferedReader</b></code>가 2번의 값을 `버퍼에 저장`했다가 `한번에 문자열로 반환`한다.
<br>

> StringTokenizer의 <code><b>nextToken()</b></code> 함수를 쓰면 readLine()을 통해 입력 받은 값을 공백 단위로 구분하여 순서대로 호출할 수 있다.
<br>

> <code><b>split()</b></code>을 사용하면, 입력받은 값을 `공백단위`로 끊어 `배열에 데이터를 저장`한다.




<br><br><br>

### - 대표 메서드

|메서드	| 리턴타입| 설명|
|:---:|:---:|:---:|
|read() | int| 문자 하나를 읽어 int형으로 리턴<br>ex) '3'을 읽고 정수형인 (int)'3' = 51로 반환|
|readLine()	| String|한 줄의 문자열을 읽음|
|skip(n)|long |n개의 문자를 스킵하고 넘어감|
|close()|void|입력 스트림을 닫고, 사용하던 자원을 해제|

<br><br><br><br>

## 3. BufferedWriter 클래스
일반적으로 출력을 할 때는 `System.out.println("");`을 사용하는데, 적은 양의 출력에서는 편리하다.<br> 하지만 `BufferedWriter`는 버퍼를 사용하기 때문에 `속도와 성능`면에서 더 뛰어나고, `많은 양의 데이터`를 처리할 때 이득이다.<br><br>

그러나 `System.out.println();`처럼 출력과 개행을 동시에 해주지 않기 때문에, 개행이 필요한 경우에는 반드시 `bw.write("\n") `혹은 `newLine()` 메서드를 사용해야 한다.<br><br>
또한, BufferedWriter 의 경우 버퍼를 잡아 놓았기 때문에 반드시 `flush() / close()` 를 반드시 호출해 주어 버퍼를 클린하게 해줘야 한다.


<br><br><br>

### - BufferedWriter 사용법
```java
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.OutputStreamWriter;

public class Main {
                                          	//예외처리 필수
	public static void main(String[] args) throws IOException {
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));  //BufferedWriter 객체 선언
		String s = "abcdefg";  
		bw.write(s+"\n");  
		//bw.newLine();
		bw.flush();  //버퍼에 남아있는 데이터를 모두 출력
		bw.close();  //스트림을 닫음
	}
}
```
> <div class="color">주의!!</div>
> <code><b>.write()</b></code>만 사용한다고 콘솔에 출력되는 것이 아니라 `flush()`를 사용해 버퍼를 비우는 동시에 출력해야 한다.<br>
> BufferedWriter 역시 BufferedReader와 마찬가지로 <code><b>IOException 예외 처리</b></code>를 반드시 해 주어야 한다.

<br><br><br>

### - 대표 메서드

|메서드	| 리턴타입| 설명|
|:---:|:---:|:---:|
|write(int c)| void| int형을 문자 데이터로 바꿔<br> 출력문자 스트림으로 출력|
|write(char[] cbuf,int offset,int length)| void| 문자배열에서 offset위치부터<br> length만큼 출력스트림으로 출력|
|write(String s,int offset,int length)| void| 문자열에서 offset위치부터<br> length만큼 출력스트림으로 출력|
|newLine()| void| 개행|
|flush()| void|남아있는 데이터를 모두 출력해서<br> 스트림을 비움|
|close()|void|입력 스트림을 닫고,<br> 사용하던 자원을 해제|

<br><br><br>

<span class="color">관련 페이지</span><br>
- [Scanner 클래스](/java/Scanner 클래스/)

---
참고링크 | <br>
[크크님 blog](https://rlakuku-program.tistory.com/33)
<br><br><br>