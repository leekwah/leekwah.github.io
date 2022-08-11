---
title: import문
categories:
  - Develop
tags:
  - Java
  - OOP
  - 자바의 정석 기초편
---
# import문

클래스를 사용할 때 패키지이름을 생략할 수 있다.
컴파일러에게 클래스가 속한 패키지를 알려준다.
이클립스 단축키로는 Ctrl + Shift + O 이다.

예를 들 때,원래는 date 클래스일 때, class이름을 써야한다.

```java
class ImportTest {
    java.util.Date today = new java.util.Date();
}
```

하지만, import문을 쓰면 생략이 가능하다.

```java
import java.util.Date;

class ImportTest {
	Date today = new Date();
}
```

**java.lang 패키지의 클래스는 import하지 않고도 사용할 수 있다.**
**String, Object, System, Thread, ...** 

```java
import java.lang.*; // *은 모든 클래스를 의미한다. System이나 String때, 원래 써야하지만 생략가능하다.
class ImportTest2 {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```

## import문의 선언

import문은 패키지문과 클래스선언의 사이에 선언한다.
import문은 컴파일 시에 처리되므로 프로그램의 성능에 영향이 없다.
import문을 선언하는 방법은 다음과 같다.

```java
import 패키지명.클래스명; // 이클립스는 자동으로 이렇게 만들어준다.
// 또는
import 패키지명.* // *은 모든클래스를 의미한다.
```

```java
package com.codechobo.book;

import java.text.SimpleDataFormat;
import java.util.*;

public class PackageTest {
    public static void main(String[] args) {
        // java.util.Date today = new java.util.Date();
        Date today = new Date();
        SimpleDateFormat date = new SimpleDateFormat("yyyy/MM/dd");
    }
}
```

다음의 두 코드는 의미가 다르다.

```java
import java.util.*;
import java.text.*;
```

```java
import java.*; // java의 패키지의 모든 클래스 (패키지는 포함 안됨)
```

이름이 같은 클래스가 두 패키지를 import할 때는 클래스 앞에 패키지명을 붙여줘야 한다.

```java
import java.sql.*; // java.sql.Date
import java.util.*; // java.util.Date

public class ImportTest {
    public static void main(String[] args) {
        java.util.Date today = new java.util.Date(); // 클래스 앞에 이름필요
    }
}
```

## static import


static멤버를 사용할 때, 클래스 이름을 생략할 수 있게 해준다.

```java
import static java.lang.Integer.*; // Integer 클래스의 모든 static 메서드
import static java.lang.Math.random;  // Math.random()만. 괄호 안붙임.
import static java.lang.System.out; // System.out을 out만으로 참조 가능
```

위의 클래스 이름들을 아래와 같이 바뀌게 해준다.

```java
out.println(randon());
```

예제 7-6

```java
import static java.lang.System.out; // System.out을 out만으로 참조 가능
import static java.lang.Math.*; // Math 클래스의 모든 static 멤버를 클래스 이름 없이 사용 가능

class Ex7_6 {
	public static void main(String[] args) {	
		out.println(random()); // System.out.println(Math.random());
		out.println("Math.PI :" + PI); // System.out.println("Math.PI :"+Math.PI);
	}
}
```

