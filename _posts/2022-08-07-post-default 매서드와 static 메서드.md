---
title: default 매서드와 static 메서드
categories:
  - Develop
tags:
  - Java
  - OOP
  - Chapter7
---
## default 매서드와 static 메서드

인터페이스에 (default) 메서드, static메서드 추가 가능(JDK 1.8 부터)
인터페이스에 새로운 메서드(추상 메서드)를 추가하기 어려움
해결책 => 디폴트 메서드 (default method)

```java
interface MyInterface {
  void method();
  void newMethod(); // 추상 메서드
}
```

디폴트 메서드는 인스턴스 메서드(인터페이스 원칙 위반)

```java
interface MyInterface {
  void method();
  default void newMethod(); // 디폴트 메서드
}
```

### 디폴트 메서드가 기존의 메서드와 충돌할 때의 해결책

그냥 직접 오버라이딩하면 해결된다.

1. 여러 인터페이스의 디폴트 메서드 간의 충돌
   - 인터페이스를 구현한 클래스에서 디폴트 메서드를 오버라이딩해야 한다.
2. 디폴트 메서드와 조상 클래스의 메서드 간의 충돌
   - 조상 클래스의 메서드가 상속되고, 디폴트 메서드는 무시된다.