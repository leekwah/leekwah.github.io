---
title: hashCode(), toString()
categories:
  - Develop
tags:
  - Java
  - 자바의 정석 기초편
---
## hashCode()

객체의 해시코드(hash code)를 반환하는 메서드이다.<br>
Object클래스의 hashCode()는 객체의 주소를 int로 변환해서 반환한다.

```java
public class Object {
    ...
		public navtive int hashCode(); // 내용 X 네이티브 메서드 : OS의 메서드 (C언어)
}
```

equals()를 오버라이딩하면 hashCode()도 오버라이딩해야 한다.<br>
equals()의 결과가 true인 두 객체의 해시코드는 같아야 하기 때문이다.<br>

```java
public class Ex9_3 {
    public static void main(String[] args) {
        String str1 = new String("abc");
        String str2 = new String("abc");

        System.out.println(str1.equals(str2)); // true 출력
        System.out.println(str1.hashCode()); // 96354 출력
        System.out.println(str2.hashCode()); // 96354 출력
        // System.identifyHashCode(Object obj)는 Object클래스의 hashCode()와 동일하다.
        System.out.println(System.identityHashCode(str1)); // 589431969 출력
        System.out.println(System.identityHashCode(str2)); // 1252169911 출력
        // 참고 32bit JVM은 주소가 int 범위 이내이다.
        // 하지만 64bit JVM은 주소가 long타입 범위 이내이기에 겹치는 주소가 있을 수도 있다.
    }
}
```

## toString()

객체를 문자열(String)으로 변환하기 위한 메서드이다.

```java
public String toString() {
		return getClass().getName()+"@"+Integer.toHexString(hasCode());
  				// 반환 설계도객체().클래스이름()+at(위치).정수.16진.(객체주소)
}
```

대부분은 다르지만, 오버라이징하면 같을 수도 있다. (가능성)

예제 Ex9_4

```java
package ch09;

class Card {
    String kind;
    int number;

    Card() {
        this("SPADE", 1);
    }

    Card(String kind, int number) {
        this.kind = kind;
        this.number = number;
    }
}

class Ex9_4 {
    public static void main(String[] args) {
        Card c1 = new Card();
        Card c2 = new Card();

        System.out.println(c1.toString()); // Card@232204a1
        System.out.println(c2.toString()); // Card@4aa298b7
    }
}
```

equals가 true일 때는 hashCode값이 같게 나온다.

```java
import java.util.Objects;

class Card {
    String kind;
    int number;

    Card() {
        this("SPADE", 1);
    }

    Card(String kind, int number) {
        this.kind = kind;
        this.number = number;
    }
    public String toString() {
        return "kind : "+ kind + ", number : " + number;
    }
    // equals()를 오버라이딩하면 hashCode()도 오버라이딩 해야한다.
    public int hashCode() {
        return Objects.hash(kind, number); // return Object"s"인 것을 주의해야한다.
        // 매개변수가 가변인자라서, 여러개 넣어도 된다.
    }

    // 오버라이딩을 할 때는 선언부가 일치해야한다.
    public boolean equals(Object obj) {
        if (!(obj instanceof Card))
            return false;

        Card c = (Card)obj;
        return this.kind.equals(c.kind) && this.number == c.number;
    }
}

class Ex9_4 {

    public static void main(String[] args) {
        Card c1 = new Card();
        Card c2 = new Card();

        System.out.println(c1.equals(c2));

        System.out.println(c1.toString()); // kind : SPADE, number : 1 출력
        System.out.println(c2.toString()); // kind : SPADE, number : 1 출력

        // equals가 true일 때는 hashCode값이 같게 나온다.
        System.out.println(c1.hashCode()); // -1842861219 출력
        System.out.println(c2.hashCode()); // -1842861219 출력
    }
}
```

