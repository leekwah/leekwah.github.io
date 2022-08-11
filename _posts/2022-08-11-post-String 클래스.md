---
title: String 클래스
categories:
  - Develop
tags:
  - Java
  - 자바의 정석 기초편
---
## String 클래스

문자열을 다루기 위한 클래스 = 데이터(char[] : 문자배열) + 메서드(문자열 관련)<br>내용을 변경할 수 없는 불변(immutable)클래스이다.

```java
public final class String implements java.io.Serializable, Comparable {
  	private char[] value;
  	...
}
```

덧셈 연산자(+)를 이용한 문자열 결합은 성능이 떨어진다. <br>문자열의 결합이나 변경이 잦다면, 내용을 변경가능한 StringBuffer를 사용한다.

### 문자열의 비교

String str = "abc ";와 String str = new String("abc");의 비교

```java
String str1 = "abc"; // 문자열 리터럴 "abc"의 주소가 str1에 저장됨
String str2 = "abc"; // 문자열 리터럴 "abc"의 주소가 str2에 저장됨
String str3 = new String("abc"); // 새로운 String 인스턴스를 생성
String str4 = new String("abc"); // 새로운 String 인스턴스를 생성
```

![20220811_2](/assets/img/20220811_2.png)

new연산자를 사용하면, 항상 **<u>새로운</u>** 문자열이 만들어진다. <br>그렇기 때문에, 등가비교연산자로 비교하지 않고, <u>equals()를 이용해서 비교</u>한다.<br>new연산자를 이용해서 만든 것은 같은 문자열이라도, 새로운 객체로 만들어진다.

```java
str1 == str2 ? true // 주소비교
str1.equals(str2) ? true // 내용비교
  
str3 == str4 ? false // 주소비교
str1.equals(str2) ? true // 내용비교
```

### 문자열 리터럴

문자열 리터럴은 프로그램 실행시 자동으로 생성된다. (constant pool에 저장 - 상수 저장소)<br>

```java
class Ex9_7 {
		public static void main (String args[]) {
      	String s1 = "AAA";
      	String s2 = "BBB";
      	String s3 = "AAA";
      	String s4 = "BBB";
    }
}
```

![20220811_3](/assets/img/20220811_3.png)

같은 내용의 문자열 리터럴은 하나만 만들어진다.<br>문자열리터럴(String 객체) - 리터럴은 상수이다.<br>**<u>불변 = 내용변경 불가능</u>**이기 때문에, 여러개의 참조변수가 하나의 String객체를 공유해도 문제가 되지 않는다.

### 빈 문자열(empty string, "")

내용이 없는 문자열이며, 크기가 0인 char형 배열을 저장하는 문자열이다.

```java
String str = ""; // str을 빈 문자열로 초기화
```

크기가 0인 배열을 생성하는 것은 어느 타입이나 가능하다.

```java
char[] chArr = new char[0]; // 길이가 0인 char배열
int[] iArr = {}; // 길이가 0인 int배열
```

문자(char)와 문자열(String)의 초기화는 다음과 같이 선언한다.

```java
String s = ""; // 빈 문자열로 초기화
char c = ' '; // 공백으로 초기화
```

String str = new String("");은 좋지 않은 초기화이다.<br>그 이유는 빈 문자열을 계속 만들게 되기 때문이다.<br>**<u>String str = "";</u>**을 쓰는 것이 더 좋다.
