---
title: super
categories:
  - Develop
tags:
  - Java
  - 상속
  - Chapter7
---
# 참조변수 super

객체 자신을 가리키는 참조변수, this와 비슷하다. <u>인스턴스 메서드(생성자)내에만</u> 존재한다. (static 메서드 내에서 사용 불가능)
**this**는 **lv와 iv구별에 사용**했지만, **super**는 **조상의 멤버와 자신의 멤버를 구별할 때 사용**한다.
이름이 겹칠 때는, 상속이 된다.
둘 다 존재한다.
**super와 this로 구별한다.**
**<u>조상멤버에는 super</u>**를 붙이고, **<u>자기멤버에는 this</u>**

예제 7-2

```java
class Ex7_2 {
	public static void main(String args[]) {
		Child c = new Child();
		c.method();
	}
}

class Parent { int x=10; /* super.x */ }

class Child extends Parent {
	int x=20; // this.x

	void method() {
		System.out.println("x=" + x); // 20
		System.out.println("this.x=" + this.x); // 20
		System.out.println("super.x="+ super.x); // 10
	}
}
```

예제 7-3
조상멤버기도 하지만, 내꺼기도 하기 때문에 중복가능하다.
<u>super라는 참조변수와 this라는 참조변수가 같은 주소를 가리키고 있다고 생각하면 된다.</u>

```java
class Ex7_3 {
	public static void main(String args[]) {
		Child2 c = new Child2();
		c.method();
	}
}

class Parent2 { int x=10; /* super.x와 this.x 둘 다 가능 */ }

class Child2 extends Parent2 {
	void method() {
		System.out.println("x=" + x); // 10
		System.out.println("this.x=" + this.x); // 10
		System.out.println("super.x="+ super.x); // 10
	}
}
```

# 조상의 생성자 - super()

조상의 생성자를 호출할 때 사용한다. <u>this()처럼 생성자</u>이다.
자손클래스의 생성자에서 조상클래스의 생성자를 호출할 일이 있다.
**<u>상속에서 생성자 초기화불럭은 상속이 안된다.</u>** 
조상의 멤버는 조상의 생성자를 호출해서 초기화한다.
**<u>자손의 클래스에서, 조상의 클래스를 호출할 때 사용한다.</u>**

```java
class Point {
	int x, y;
	
	Point(int x, int y) {
		this.x = x; // iv 초기화
		this.y = y; // iv 초기화
	}
}
```

상속을 했을 경우에는, 아래와 같이 초기화한다고 생각하면 된다.
하지만, 에러는 아니지만 옳지 않은 방법이다.

```java
class Point3D extends Point {
	int z;
	
	Point3D(int x, int y, iuntz) { // 자손의 생성자
        this.x = x; // 조상의 멤버를 초기화(에러는 아니지만, 옳지않은 방법)
        this.y = y; // 조상의 멤버를 초기화(에러는 아니지만, 옳지않은 방법)
        this.z = z; // iv 초기화
	}
}
```

그렇기에 아래와 같이 super를 이용해서 초기화를 해야한다.

```java
class Point3D extends Point {
	int z;
	
	Point3D(int x, int y, int z) {
        super(x,y); // 조상클래스의 생성자
		// Point(int x, int y를 호출 후 조상의 클래스가 초기화 하도록)
        this.z = z; // 자신의 멤버를 초기화
	}
}
```

<span style="color:red">**생성자의 첫 줄에 <u>반드시 생성자를 호출</u>해야 한다.**</span>
**그렇지 않으면, 컴파일러가 생성자의 첫 줄에 super();를 삽입한다.**

```java
class Point {
	int x;
	int y;
	
	Point() {
		this(0,0); // 생성자 활용했음 (여기서는 this호출)
	}
	
	Point(int x, int y) {
		this.x = x;
		this.y = y;
	}
}
```

컴파일러가 생성자의 첫 줄에 super를 삽입했다.

```java
class Point {
	int x;
	int y;
	
	Point() {
		this(0,0); // 생성자 활용했음
	}
	
	Point(int x, int y) {
		super(); // Object(); (여기서는 super 호출)
		this.x = x;
		this.y = y;
	}
}
```

# 생성자 예제

```java
public class Ex7_4 {
	public static void main(String[] args) {
		Point3D p = new Point3D(1, 2, 3);
		System.out.println("x=" + p.x + ",y=" + p.y + ",z=" + p.z);
	}
}

class Point {
	int x, y;

	Point(int x, int y) {
		this.x = x;
		this.y = y;
	}
}

class Point3D extends Point {
	int z;

	Point3D(int x, int y, int z) {
		super(x, y); // Point(int x, int y)를 호출
		this.z = z;
	}
}
```