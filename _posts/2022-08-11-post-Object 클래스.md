---
title: Object 클래스
categories:
  - Develop
tags:
  - Java
  - 자바의 정석 기초편
---
## Object 클래스

모든 클래스의 최고조상으로 오직 11개의 메서드만을 가지고 있다.
notify()와 wait()는 쓰레드와 관련된 메서드이다.

`![20220811_1](/assets/img/20220811_1.png)

**protected 되어 있는 것들은 <u>오버라이딩을 해서 public으로 변경</u>해야한다.**

finalize()는 마무리작업을 하는 것이지만, 메모리 정리하느라 시간이 많이 소요됨 -> 잘 사용하지 않게 됨
getClass()의 클래스정보는 설계도 정보이다.
Class에서 대문자는 클래스의 정보를 담기위한 것이다.
ReflectionAPI를 통해서,

### equals(Object obj)

반환타입은 boolean, 객체 자신(this)과 주어진 객체(obj)를 비교한다. 같으면 true, 다르면 false를 출력한다.
Object 클래스의 equals()는 객체의 주소를 비교 (참조변수 값 비교)

```java
public boolean equals (Object obj) {
  	return (this==obj);
}
```

예제 Ex9_1를 통해서 equals (Object obj) 좀 더 자세히 알아보기

```java
public class Ex9_1 {
    public static void main(String[] args) {
        Value v1 = new Value(10);
        Value v2 = new Value(10);

        if (v1.equals(v2)) // 이 값이 false라서 
            System.out.println("v1과 v2는 같습니다.");
        else
            System.out.println("v1과 v2는 다릅니다.");
    } // main
}

class Value {
    int value;

    Value(int value) {
        this.value = value;
    }
}

// 결과 : v1과 v2는 다릅니다.
```

같게 만들려면 아래와 같이 하면 된다. 그리고, 주의점은 다음과 같다. <br> 참조변수의 형변환 전에는 반드시 instanceof로 확인해야 한다.<br>객체의 주소를 비교 (참조변수 값 비교)하기 위해서는 형변환이 필요하다.

```java
package ch09;

public class Ex9_1 {
    public static void main(String[] args) {
        Value v1 = new Value(10);
        Value v2 = new Value(10);

        if (v1.equals(v2))
            System.out.println("v1과 v2는 같습니다.");
        else
            System.out.println("v1과 v2는 다릅니다.");
    } // main
}

class Value {
    int value;

    Value(int value) {
        this.value = value;
    }

    // Object의 equals()를 오버라이딩해서 주소가 아닌 value를 비교
    public boolean eqauls(Object obj) {
        // return this == obj; 는 주소비교이다. 서로 다른 객체는 항상 거짓이다.
        // 참조변수의 형변환 전에는 반드시 instanceof로 확인해야 한다.
        if(!(obj instanceof Value)) return false;

        // obj에는 value가 없으므로, 형변환 필요
        Value v = (Value)obj;

        return this.value == v.value;
    }
}
```

equals(Object obj)의 오버라이딩

인스턴스 변수(iv)의 값을 비교하도록 equlas()를 오버라이딩 해야한다.

```java
class Persion {
  	long id;
  
  	public boolean equals (Object obj) {
      	if (obj instanceof Person)
          	return id ==((Person)obj.id);
      			// obj가 Object타입이므로, id값을 참조하기 위해서는 Person으로 형변환이 필요하다.
      	else
          	return false; // 타입이 Person이 아니면, 비교할 필요가 없다.
    }
  
  	Person (long id) {
      	this.id = id;
    }
}
```

다음의 아래 두 코드는 같은 코드이다.

```java
class Person {
    long id;

    public boolean equals(Object obj) {
        if(obj instanceof Person)
            return id ==((Person)obj).id;
            // obj가 Object타입이므로, id값을 참조하기 위해서는 Person으로 형변환이 필요하다.
        else
            return false; // 타입이 Person이 아니면, 비교할 필요가 없다.
    }

    Person(long id) {
        this.id = id;
    }
}

class Ex9_2 {
    public static void main(String[] args) {
        Person p1 = new Person(8011081111222L);
        Person p2 = new Person(8011081111222L);

        if (p1.equals(p2))
            System.out.println("p1과 p2는 같은 사람입니다.");
        else
            System.out.println("p1과 p2는 다른 사람입니다.");
    }
}

// 결과 p1과 p2는 같은 사람입니다.
```

```java
class Person {
    long id;

    public boolean equals(Object obj) {
        if(!(obj instanceof Person)) // 타입이 Person이 아니면, 비교할 필요가 없다.
            return false;
        // obj가 Object타입이므로, id값을 참조하기 위해서는 Person으로 형변환이 필요하다.
      	Person p = (Person)obj;
				return this.id == p.id;
    }

    Person(long id) {
        this.id = id;
    }
}

class Ex9_2 {
    public static void main(String[] args) {
        Person p1 = new Person(8011081111222L); 
        Person p2 = new Person(8011081111222L);

        if (p1.equals(p2)) // true이면 나오는 값
            System.out.println("p1과 p2는 같은 사람입니다.");
        else // false이면 나오는 값
            System.out.println("p1과 p2는 다른 사람입니다.");
    }
}

// 결과 p1과 p2는 같은 사람입니다.
```

