---
title: "[java] Arrays.sort() 를 이용한 배열 정렬"
#excerpt: "본문의 주요 내용을 여기에 입력하세요"

categories:
  - Java
tags:
  - [java, 정렬]

permalink: /java/Arrays.sort() 를 이용한 배열 정렬/



date: 2023-08-07
#last_modified_at: 2021-10-09
---

## 1. Arrays.sort()
Arrays 클래스는 "배열의 복사, 항목 정렬, 검색" 과 같은 배열 조작 기능을 가지고 있다. <br>
자바에서 <code>배열이나 리스트를 정렬</code> 하는 경우 <span class="color">java.util.Arrays 클래스의 sort() 메서드</span> 를 사용한다.<br>
오름차순, 내림차순 정렬이 모두 가능하다.
<br><br><br><br>

---

## 2. 배열의 오름차순 정렬
Arrays.sort() 메서드의 매개값으로 <code>기본 타입 배열이나 String 배열</code>을 지정해주면 자동으로 오름차순 정렬이 된다.<br><br><br>
```java
import java.util.Arrays;

public class Main {

	public static void main(String[] args) {
				 
		int[] intArr = {1,3,5,2,4}; // 또는 new int[] {1,3,5,2,4}                                          
		double[] doubletArr = {1.1, 3.3, 5.5, 2.2, 4.4};       
		String[] stringArr = {"A","C","F","E","B","D"};

		// 전체 정렬
		Arrays.sort(intArr); // [1,2,3,4,5]        
		Arrays.sort(doubletArr); // [1.1,2.2,3.3,4.4,5.5]       
		Arrays.sort(stringArr); // [A,B,C,D,E,F]      
	}
}
```

<br><br><br><br>

---

## 3. 배열의 내림차순 정렬
<code><b>sort의 인자</b></code>로 <code>배열</code>과 <code>Comparator 객체</code>를 전달하면 원하는대로 정렬이 가능하다.<br>
만약 기본 타입 배열을 내림차순으로 정렬하고 싶다면 기본 타입의 배열을 <code><b>래퍼클래스</b></code>로 만들고 <code><b>Comparator를 두번째 인자</b></code>에 넣어줘야 한다.<br>
배열을 내림차순으로 정렬할 경우에 사용되는 Comparator는 <span class="color">Collections 클래스의 reverseOrder() 함수</span>이다. <br><br>




<div class="box">
주의!<br>
byte, char, double, short, long, int, float같은 PrimitiveType의 배열에는 적용이 불가능하니<br> <code><b>Integer같은 Wrapper "Class"</b></code>를 이용해야 한다는 점이다.<br><br>
String은 기본 타입이 아니다.
</div>
<br>

```java
import java.util.Arrays;

public class Main{

    public static void main(String[] args)  {

        Integer arr[] = {6,21,19,35,26}; // 래퍼 클래스
        Arrays.sort(arr,Collections.reverseOrder());
        
        for (int i : arr) {
            System.out.print("["+i+"]"); // [35][26][21][19][6]
        }
    }
}
```

<br><br><br>

---

## 4. 배열의 일부분만 정렬
Arrays.sort()메서드의 매개값으로 <code><b>배열, 시작 index, 끝 index</b></code> 를 넣어주면 일부분만 정렬할 수 있습니다.<br><br><br>

```java
import java.util.Arrays;

public class Main{
   public static void main(String[] args)  {
        int arr[] = {4,23,33,15,17,19};

        Arrays.sort(arr, 0, 4); // 0,1,2,3 요소만 정렬
        
         System.out.print(Arrays.toString(arr)); // [35, 26, 21, 17, 19]
    }
}
```
> Arrays 클래스의 <code><b>toString() 메서드</b></code> 는 배열을 <code><b>문자열로 반환</b></code>하는 역할을 한다.<br>
이 메서드는 배열의 요소들을 [ ] 괄호로 둘러싸고, 각 요소들을 쉼표(,)로 구분하여 하나의 문자열로 만들어 준다.

<br><br><br>

---

## 5. 객체 배열 정렬
<br>

### 5-1. 객체 정렬 기준의 필요성
int 나 char 와 같은 기본형(primitive) 데이터는 사람들이 당연하게 받아들이는 대소 비교라는 개념이 있다. 우리는 1보다는 2가 크며, 'A' 보단 'B'가 크다는 것을 알기 때문에 자바는 이런 통념에 따라 알아서 정렬을 해준다.<br><br>

하지만 특정 타입의 객체는 기본형 데이터와 달리 정렬 기준이 없으면 정렬을 할 수가 없으며, 따라서 정렬 기준을 정의하여 알려줘야 한다.

객체로 이루어진 배열의 경우, 객체 클래스는 <code><b>Comparable 인터페이스의 compareTo() 메서드</b></code> 를 재정의해야 한다. 

<br><br><br><br>

### 5-2. Comparable 인터페이스 사용
객체의 정렬 기준을 정의하는 첫번째 방법은,<br>
정렬 대상 클래스가 자바에서 제공하는 <code><b>Comparable 인터페이스를 구현 (implements)</b></code> 하도록 하는 것이다. 
<br><br><br>
Comparable 인터페이스의 <code><b>compareTo() 메서드</b></code> 를 통해 인자로 넘어온 객체는 같은 타입의 다른 객체와 <code><b>대소 비교가 가능하다.</b></code><br><br> 
- 반환값이 양수 : <u>현재 객체가</u> 인자로 넘어온 객체보다 <u>크다</u> 는 것을 의미한다.
- 반환값이 음수 : <u>현재 객체가</u> 인자로 넘어온 객체보다 <u>작다</u> 는 것을 의미한다.
- 반환값이 0 : <u>현재 객체와</u> 인자로 넘어온 객체가 <u>동일하다</u> 는 것을 의미한다.
<br><br><br>

예를 들어 보자.<br>
```java
public class Student implements Comparable<Student> {
    private String name;
    private int score;

    public Student(String name, int score) {
        this.name = name;
        this.score = score;
    }
    // Getters, Setters 생략
	
    @Override
    public int compareTo(Student s) {
	// 메서드의 반환 값은 현재 객체와 인자로 넘어온 객체(s)의 비교 결과를 나타낸다.
	return s.getScore() - getScore(); 
    }
}
```
> 예를 들어 인자로 넘어온 학생의 점수가 82이고 compareTo() 메서드를 호출하는 객체의 점수가 98이라면, <code><b>compareTo() 메서드는 음수(82-98)를 리턴</b></code> 하게 된다.<br> 
즉, <code><b>메서드를 호출하는 학생이</b></code> 인자로 넘어온 학생보다 <code><b>작다</b></code> 는 것을 의미한다. <br><br>
결과적으로 메서드를 호출하는 현재 객체가 점수는 더 크지만, <u>객체 자체 비교에서는 반환값이 음수이기 때문에 현재 객체가 더 작다고 간주되어 앞부분에 위치한다.</u>

<br><br><br>

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("Alice", 85));
        students.add(new Student("Bob", 92));
        students.add(new Student("chloe", 78));

        Collections.sort(students); // 학생들의 점수를 기준으로 내림차순 정렬
        System.out.println(students); // 리스트 출력
        // [Student(name=Bob, score=92), Student(name=Alice, score=85), Student(name=chloe, score=78)]
    }
}
```
> <code><b>Collections.sort() 메서드</b></code>는 <code><b>리스트나 컬렉션</b></code>과 같은 동적인 데이터 구조에 대해서 주로 쓰이는 방식이다.

> Collections.sort(players) 메서드가 실행되면 정렬 알고리즘에 의해 <code><b>compareTo 메서드가 내부적으로 호출된다.</b></code><br>
 첫 번째 호출에서는 Alice 객체와 Bob 객체가 compareTo 메서드를 통해 비교되는데, 현재 객체가 Alice 이며 인자로 들어오는 객체가 Bob 이다.<br>

>  정렬 후 학생 리스트를 출력해보면 원하는 바와 같이 점수가 제일 높은 Bob 이 리스트의 맨 앞으로 위치하고, 점수가 제일 낮은 chloe 가 리스트의 맨 뒤에 위치하게 된다.

<br><br><br><br>

---
### 5-3. Comparator 객체 사용
만약 정렬 대상 클래스의 코드를 직접 수정할 수 없는 경우에는 어떻게 객체의 정렬 기준을 정의할 수 있을까?<br> 
또는 정렬 하고자 하는 객체에 이미 존재하고 있는 정렬 기준과 다른 정렬 기준으로 정렬을 하고 싶을 때는 어떻게 해야할까?<br><br>

이 때 필요한 것이 바로 <code><b>Comparator 인터페이스</b></code> 이다.<br>
Comparator 인터페이스의 구현체를 Arrays.sort()나 Collections.sort()와 같은 정렬 메서드의 추가 인자로 넘기면, <code><b>정렬 기준이 누락된 클래스의 객체를 정렬하거나</b></code> 기존 정렬 기준을 무시하고 <code><b>새로운 정렬 기준으로 객체를 정렬할 수 있다.</b></code><br><br>

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("Alice", 85));
        students.add(new Student("Bob", 92));
        students.add(new Student("chloe", 78));
		
        Comparator<Student> comparator = new Comparator<Student>() {
            @Override
            public int compare(Student a, Student b) {
                return b.getScore() - a.getScore();
            }
        };

        Collections.sort(students, comparator); 
        System.out.println(students);
        // [Student(name=Bob, score=92), Student(name=Alice, score=85), Student(name=chloe, score=78)]
    }
}
```
> Comparator 객체를 Collections.sort() 메서드의 두번째 인자로 넘긴다.<br>
정렬 대상 객체가 Comparable 인터페이스 구현 여부와 상관없이, 넘어온 Comparator 구현체의 compare() 메서드 기준으로 정렬을 수행한다. 

> compare() 메서드는 비교 대상 2 개의 객체를 인자를 차례로 인자로 받는다.<br>
 첫번째 인자가 두번째 인자보다 작다면 음수, 같다면 0, 크다면 양수를는턴하면 된다.

<br><br><br>

#### - 람다 함수로 대체
람다 함수는 추상 메서드가 하나만 있는 인터페이스에서만 사용할 수 있다.<br>
Comparator 객체는 <code>메서드가 하나 뿐인 함수형 인터페이스를 구현하기 때문에</code> 람다 함수로 대체가 가능하다.

```java
Collections.sort(students, (a, b) -> b.getScore() - a.getScore());
System.out.println(students);
```
코드가 훨씬 간결해진 것을 볼 수 있다.

<br><br><br><br>

---
참고링크 | <br>
- [java Arrays.sort()에 대해서 알아보자](https://velog.io/@skwx50000/java-Arrays.sort%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90)
- [자바 배열 정렬하기(오름차순, 내림차순) Arrays.sort()](https://coding-factory.tistory.com/549)
- [객체 정렬하기 1부 - Comparable vs Comparator](https://www.daleseo.com/java-comparable-comparator/)
<br><br><br>