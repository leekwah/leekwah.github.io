---
published: true
title: chapter6
comments: null
read_time: true
layout: tags
author_profile: true
---
## 클래스의 정의 - 1 설계도

### 클래스(설계도) 필요 이유

​	제품(객체)를 사용하기 위해서

### 객체 필요 이유

​	제품(객체)를 사용하기 위해서

### 객체 사용 의미는?

​	속성(변수)과 기능(메서드)을 사용

### 하나의 소스 파일에 여러 클래스 작성

​	**<u>public class가 있는 경우</u>**, <u>**반드시**</u> puiblic class의 이름과 **<u>일치해야 한다.</u>** 또한, public class는 <u>**하나만**</u> 존재할 수 있다.
​	**<u>public class가 없는 경우</u>**, 소스 파일의 이름은 class의 이름 중 아무거나 가능하다. <u>**하지만, 대소문자까지 일치해야 한다.**</u>

## 객체의 생성과 사용

### 객체의 생성

​	객체를 생성할 때는 참조 변수를 먼저 선언한 뒤에, 인스턴스를 생성하고, 생성된 인스턴스의 주소를 참조 변수에 저장한다.

```java
Tv = t;
t = new Tv();
```

​	한 문장으로 합치면 아래와 같다.

```java
Tv t = new Tv();
```

### 	객체의 사용

​	객체의 사용은 변수, 메서드를 사용한 다는 것이다.

```java
t.channel = 7;
t.channelDown();
```

## 전체적인 과정

1) 클래스 생성
   (설계도 생성)

2) 객체 생성
   (제품 생성)

3) 객체 사용
   (제품 사용) 

### 객체의 생성과 사용

​	하나의 인스턴스를 여러 개의 참조 변수가 가리키는 경우는 <u>**가능**</u>하지만, 여러 인스턴스를 하나의 참조 변수가 가리키는 경우는 <u>**불가능**</u>

### 객체배열

​	객체배열 == 참조변수 배열

```java
tv tv1, tv2, tv3;
// 다음과 같다.
Tv[] tvArr = new Tv[3]; // 길이가 3인 Tv타입의 참조변수 배열

// 객체를 생성해서 배열의 각 요소에 저장
tvArr[0] = new Tv();
tvArr[1] = new Tv();
tvArr[2] = new Tv();
// 배열 초기화를 간단히 하면 아래와 같다.
Tv[] tvArr = { new Tv(), new Tv(), new Tv() };
```

## 클래스의 정의 - 2 데이터 + 함수

클래스 == 데이터 + 함수

1. 변수 - 하나의 데이터를 저장할 수 있는 공간
2. 배열 - 같은 종류의 여러 데이터를 하나로 저장할 수 있는 공간
3. 구조체 서로 관련된 여러 데이터(종류 관계 상관 X)를 하나로 저장할 수 있는 공간
4. 클래스 데이터와 함수의 결합 (구조체 + 함수)

## 클래스의 정의 - 3 사용자 정의 타입

사용자 정의 타입 - 원하는 타입을 직접 만들 수 있다.

```java
int hour;
int minute;
int second;
```

```java
int hour1, hour2, hour3;
int minute1, minute2, minute3; 
int second1, second2, second3;
```

```java
int[] hour = new int[3];
int[] minute = new int[3];
int[] second = new int[3];
```

문제 해결을 위해서 아래 3개의 변수를 묶어서 새로운 Time이라는 클래스를 만든다. 

```java
class Time {
	int hour;
	int minute;
	int second;
}
```

그렇게 되면, 3개의 변수를 생성하는 첫 번째 코드 대신에 하나의 객체를 생성하는 걸로 대신할 수 있다. 그 이유는 클래스 Time은 3개의 변수를 하나로 묶은 것이기 때문에 같은 의미기 때문이다.

```java
Time t = new Time();
```

두 번째에 있는 코드는 아래와 같이 쓸 수 있게 된다. 3개의 시간을 다루기 위하기 때문이기 때문이다.

```java
Time t1 = new Time();
Time t2 = new Time();
Time t3 = new Time();
```

세 번째에 있는 배열은 아래와 같이 객체 배열로 바꿀 수 있게 된다.

```java
Time[] t= new Time[3];
t[0] = new Time();
t[1] = new Time();
t[2] = new Time();
```

묶게 된다면,  묶지 않았을 때보다 코드 간결화가 일어나게 된다. 또한 유지보수가 편해지고, 객체지향적인 코드이다.

