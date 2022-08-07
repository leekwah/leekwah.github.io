---
title: 오버라이딩 (overriding)
categories:
  - Develop
tags:
  - Java
  - 상속
  - OOP
  - Chapter7
---
# 오버라이딩 (overriding)

상속받은 조상의 메서드를 자신에 맞게 변경하는 것이다. 정확히는 메서드 오버라이드이다.
override의 뜻은 덮어쓰다라는 뜻이 있다.

## 오버라이딩의 조건

1. 선언부가 조상클래스의 메서드와 일치해야한다.
2. 접근 제어자(public, protected, defaul, private)를 조상 클래스의 메서드보다 좁은 범위로 변경할 수 없다.
3. 예외(8장)는 조상 클래스의 메서드보다 많이 선언할 수 없다.

Point 클래스가 있을 때, getLocation() 이라는 메서드를 통해서, 문자열로 반환한다.
Point3D라는 Point를 상속받은 클래스가 있고, 이 클래스는 3차원 좌표상의 점을 출력하는 역할을 할 때, z라는 점이 필요하다.
하지만, Point 클래스에 있던 getLocation() 메서드를 이용할 땐, z의 위치가 반영이 되어있지 않기 때문에, 오버라이딩을 활용해야한다.
조상것의 선언부는 수정 불가능하지만, 내용만 변경가능하다. (내용 : 구현부 - 블럭)
새롭게 만들 수 있지만, 같은 일을 해야할 때는 오버라이딩을 활용하는 것이 더 낫다.

```java
class Point {
    int x;
    int y;
    String getLocation() {
        return "x :" + x + ", y :" + y;
    }
}

class Point3D extends Point {
    int z;
    String getLocation() {
        return "x :" + x + ", y :" + y + ", z : " + z;
    }
}
```

## 예제 - OverrideTest

### 오버라이딩 전

결과가 x : 3, y : 5만 나오게 된다.

```java
class MyPoint3 {
	int x;
	int y;
	String getLocation() {
		return "x:"+x+", y:"+y;
	}
}

class MyPoint3D extends MyPoint3 {
	int z;
}

public class OverridTest {
	public static void main(String[] args) {
		MyPoint3D p = new MyPoint3D();
		p.x = 3;
		p.y = 5;
		p.z = 7;
		System.out.println(p.getLocation());
	}
}

```

### 오버라이딩 후

이후에 오버라이딩을 한 뒤에는 결과가 x : 3, y : 5, z : 7로 잘 출력된다. 오버라이딩이 된 것이 호출된다. (다형성 때 다시 배운다.)

```java
class MyPoint3 {
	int x;
	int y;
	String getLocation() {
		return "x:"+x+", y:"+y;
	}
}

class MyPoint3D extends MyPoint3 {
	int z;
	// 조상의  getLocation()을 오버라이딩
	String getLocation() {
		return "x:"+x+", y:"+y+", z:"+z;
	}
}

public class OverridTest {
	public static void main(String[] args) {
		MyPoint3D p = new MyPoint3D();
		p.x = 3;
		p.y = 5;
		p.z = 7;
		System.out.println(p.getLocation());
	}
}

```

## 오버로딩 vs 오버라이딩

서로 관계는 없으나, 이름이 비슷하기 때문에 헷갈릴 수 있다.

**오버로딩(overloading)** - 기존에 없는 새로운 메서드를 정의하는 것(new) (이름이 같을 뿐, 상속과 관계 X)
**오버라이딩(overriding)** - 상속받은 메서드의 내용을 변경하는 것 (change, modify) (상속과 관계 O)