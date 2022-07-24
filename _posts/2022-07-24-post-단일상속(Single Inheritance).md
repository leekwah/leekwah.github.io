---
title: 단일상속(Single Inheritance)
categories:
  - Develop
tags:
  - Java
  - 상속
  - Chapter7
---
# 단일상속(Single Inheritance)

Java는 단일상속만을 허용한다. (C++은 다중상속을 허용한다.)
비중이 높은 클래스 하나만 상속관계로 한 뒤에, 나머지는 포함관계로 한다.

```java
class Tv {
    boolean power;
    int channel;
    
    void power() { power = !power; }
    void channelUp() { ++channel; }
    void channelDown() { --channel; }
}
```

```java
class DVD {
    boolean power;
    
    void power() { power = !power; }
    void play() { /* 내용 생략 */ }
    void stop() { /* 내용 생략 */ }
    void rew() { /* 내용 생략 */ }
    void ff() { /* 내용 생략 */ }
}
```

위와 같이 되어 있을 때, Tv안에 DVD를 상속시킨 뒤에, 객체로 생성시키면 된다.
포함이란, 객체를 생성한 뒤에, DVD가 가진 메서드를 작성한다.
작성을 하면, 껍데기만 만들어놓고, 객체가 사용하게 코드를 작성하는 것이다.
메서드를 간단히 호출하는 것이다.
메서드를 만들어주는 것이 번거롭긴 하지만, 객체를 만든 뒤에 호출해서 사용하기만 하면, 다중상속의 효과를 낼 수 있다.

```java
class TvDVD extends Tv {
	DVD dvd = new DVD();
    
    void play() {
        dvd.play();
    }
    
    void stop() {
        dvd.stop();
    }
    
    void rew() {
        dvd.rew();
    }
    
    void ff() {
        dvd.ff();
    }
}
```

# Object클래스 - 모든 클래스의 조상

부모가 없는 클래스는 자동적으로 Object클래스를 상속받게 된다.
**<u>모든 클래스는 Object클래스에 정의된 11개의 메서드를 상속**</u>받는다. (9장에서 배울 예정)
	toString(), equals(Object obj), hashCode(), ...

예를 들면, Tv클래스는 부모가 없지만, SmartTv클래스의 부모는 Tv클래스 이다.

```java
class Tv {
	// ...
}
class SmartTv extends Tv {
    // ...
}
```

컴파일을 하게 되면 컴파일러가 자동으로 extends Object를 Tv 클래스에 추가하게 된다. 

``` java
class Tv extends Object {
	// ...
}
class SmartTv extends Tv {
    // ...
}
```

