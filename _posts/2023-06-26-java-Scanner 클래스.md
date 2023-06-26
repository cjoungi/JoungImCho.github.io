---
title: "[java] Scanner 클래스"
#excerpt: "본문의 주요 내용을 여기에 입력하세요"

categories:
  - Java
tags:
  - [java, Scanner, 입출력]

permalink: /java/Scanner 클래스/



date: 2023-06-26
#last_modified_at: 2021-10-09
---

## 1. Scanner 클래스란?
Scanner 클래스는 <span class="color">java.util 패키지</span>에 있는 <span class="color">입력 클래스</span>이다.<br>
Scanner 클래스는 `문자`뿐 아니라 정수, 실수 등 `다른 자료형`도 읽을 수 있다.<br>
또한 콘솔 화면뿐 아니라 `파일`이나 `문자열`을 `생성자의 매개변수`로 받아 자료를 읽어 올 수도 있다. <br>
여러 대상에서 자료를 읽는 Scanner 클래스의 생성자는 굉장히 다양하다.<br><br>

### - 대표 생성자

|생성자	| 설명|
|:---:|:---:|
|Scanner(File source)	| `파일`을 매개변수로 받아 Scanner를 생성|
|Scanner(InputStream source) |	`바이트 스트림`을 매개변수로 받아 Scanner를 생성|
|Scanner(String source)	| `String`을 매개변수로 받아 Scanner를 생성|

<span class="color">Scanner scanner = new Scanner(System.in)</span>처럼 사용하면<br> `표준 입력`으로부터 자료를 읽어 들인다.<br><br><br>

다음은 Scanner 클래스의 다양한 메서드이다.<br>

### - 대표 메서드

|메서드	| 설명|
|:---:|:---:|
|nextBoolean() | boolean 자료를 읽는다|
|nextByte()	| byte 자료를 읽는다|
|nextShort()	| short 자료형을 읽는다|
|nextInt()	| int 자료형을 읽는다|
|nextLong()	| long 자료형을 읽는다|
|nextFloat()	| float 자료형을 읽는다|
|nextDouble()	| double 자료형을 읽는다|
|next() | 문자열 String을 읽는다 <br> 단, 띄어쓰기 전까지만 읽는다|
|nextLine()	| 문자열 String을 읽는다  <br> 띄어쓰기를 포함하여 한 줄(즉, Enter를 치기 전까지)을 읽는다|
 
<br><br><br>

## 2. Scanner의 메서드 사용시 주의할 점

### - Scanner 클래스는 <span class="color">*</span> `토큰 단위`로 데이터를 입력받는다.<br>
(단, <span class="color">nextLine()</span>은 <span class="color">Enter 단위로만</span> 데이터를 입력받는다. )

<div style="background-color:#ededed;padding:10px 20px;font-size:.8em">
<span class="color">*</span> 토큰 단위란?<br>
공백문자('', '\t', '\n')로 구분되는 요소
</div>
<br><br>
<b>예제</b>

```java
import java.util.Scanner;

public class ScannerTest {

	public static void main(String[] args) {
				
		Scanner sc = new Scanner(System.in);
		
		int number = sc.nextInt();
		double score = sc.nextDouble();
		String name = sc.next();
		String gender = sc.next();
		
		System.out.println(number + "\n" + score + "\n" + name + "\n" + gender);
		
		sc.close();
	}
}
```
<br>
<b>결과</b><br>
![result](https://github.com/cjoungi/cjoungi.github.io/assets/113075984/1f05db8e-db62-4624-b6ba-2976ca4e8572)

- 스페이스바로 구분된 토큰들은 `36, 91.5, 해피, 여자` 이므로
각 토큰들은 Scanner 메서드에 하나하나 순서대로 들어간다.
<br>
- 즉, `number에는 36`, `score에는 91.5`, `name에는 해피`, `gender에는 여자` 라는 값이 저장된다.<br><br><br><br>

### - 버퍼에서 공백문자는 사라지지 않는다.
어떤 값을 입력받을 때, 내가 입력한 `'', 't', 'n'` 값도 입력값과 `함께 버퍼에 저장`되고<br>
해당 공백문자를 다른 곳에서 읽어들이기 전까지는 `버퍼에 계속 남아있다.`<br><br><br><br>

### - nextLine() 메서드를 주의해야 한다.
nextLine() 메서드는 `Enter 단위`로 읽고, 나머지 메서드들은 토큰(Token) 단위로 읽는다.<br><br>
입력값을 읽을 경우, nextLine() 메서드는 `'\n'를 포함해서 읽어들이고,`<br>
나머지 메서드들은 공백문자를 모두 제외한 값만을 읽어들인다.<br><br>
값을 반환할 경우, nextLine() 메서드는 `'\n'를 버린 다음 값을 return 하고`<br>
나머지 메서드들은 애초에 공백문자를 제외해서 읽어들였으므로 당연히 반환값도 공백문자가 제외된 상태로 return 된다.<br><br>

<b>예제</b>

```java
import java.util.Scanner;

public class ScannerTest {

	public static void main(String[] args) {
				
		Scanner sc = new Scanner(System.in);
		
		int num = sc.nextInt();
		String str = sc.nextLine();
		
		System.out.println("num : " + num);
                System.out.println("str : " + str);
		
		sc.close();
	}
}
```
<br>
<b>결과</b><br>
![result2](https://github.com/cjoungi/cjoungi.github.io/assets/113075984/91649624-133c-40ed-a68d-9b7e819523b8)


- 이 예제에서 사용자는 `num에는 1`을 `str에는 hello`를 저장하길 원한다고 하자
- `nextInt() 메서드`는 입력값을 읽을 때 `공백문자(여기서는 Enter)를 제외`해서 읽으므로, "1"만 읽어들인다.
- 그러면 입력 버퍼에는 "1"이 나가고 "\n"만 남게 된다.
- `nextLine() 메서드`는 입력값을 읽을 때 (입력 버퍼에 저장되어있는) `공백문자를 포함`하여 읽는다.<br>
  즉, nextInt()로 인해 입력 버퍼에 저장된 "\n"까지 읽어들이는 것이다.
- 그런데 nextLine()은 Enter 단위로 값을 읽으므로, 입력 버퍼에 저장된 "\n"를 읽은 후 입력값을 모두 읽어들였다고 생각하고 넘어가버린다.<br>즉 "hello"를 입력하기도 전에 입력을 끝내버린다.
- <span class="color">결국 nextLine()은 "\n"를 버리고 반환하므로, 결국에는 아무것도 return 되지 않게 된다.</span>

<br><br><br>
<b>해결</b><br>
```java
import java.util.Scanner;

public class ScannerTest {

	public static void main(String[] args) {
				
		Scanner sc = new Scanner(System.in);
		
		int num = sc.nextInt();
                sc.nextLine(); //Enter를 버려주는 역할
		String str = sc.nextLine();
		
		System.out.println("num : " + num);
                System.out.println("str : " + str);
		
		sc.close();
	}
}
```
<br>
<b>결과</b><br>
![result2](https://github.com/cjoungi/cjoungi.github.io/assets/113075984/229894a4-ef20-47af-b0b5-ba79a3dfbb0b)


"1\n"로 인해 생긴 "\n"을 반환시에 버려주는 <span class="color">nextLine() 메서드를 중간에 작성해주면</span> 원래 의도대로 결과가 나타난다.

<br><br><br>

---
참고링크 | <br>
[CSE Pebble님 blog](https://velog.io/@cse_pebb/Java-Scanner-%EB%A9%94%EC%84%9C%EB%93%9C-%EC%B4%9D%EC%A0%95%EB%A6%AC)
<br><br><br>