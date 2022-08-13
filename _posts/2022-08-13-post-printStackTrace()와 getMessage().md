---
title: printStackTrace()와 getMessage()
categories:
  - Develop
tags:
  - Java
  - 자바의 정석 기초편
---
## printStackTrace()와 getMessage()

| printStackTrace() | 예외발생 당시의 호출스택(Call Stack)에 있었던 메서드의 정보와 예외 메시지를 화면에 출력한다. |
| ----------------- | ------------------------------------------------------------ |
| **getMessage()**  | **발생한 예외클래스의 인스턴스에 저장된 메시지를 얻을 수 있다.** |

```java
try {
		...
    System.out.println(0/0); // 예외발생
    ...
} catch (ArithmeticException ae) { // 참조변수 ae가 있고, scope가 여기부터 끝날 때 까지
    ae.printStackTrace();
    System.out.println(ae.getMessage()); // 여기까지 
} catch (Exception e) {
    ...
}
```

### printStackTrace()와 getMessage() 예제 Ex8_5

```java
class Ex8_5 {
	public static void main(String args[]) {
		System.out.println(1);			
		System.out.println(2);

		try {
			System.out.println(3);
			System.out.println(0/0); // 예외발생!!!
			System.out.println(4);   // 실행되지 않는다.
		} catch (ArithmeticException ae)	{
			// 참조변수 ae를 통해서, 생성된 ArithmeticException인스턴스에 접근할 수 있다.
			ae.printStackTrace();
			System.out.println("예외메시지 : " + ae.getMessage());
		}	// try-catch의 끝
		System.out.println(6);
	}	// main메서드의 끝
}

// 결과 1
// 2
// 3
// 예외메시지 : / by zero
// 6
// java.lang.ArithmeticException: / by zero
// 	at ch08.Ex8_5.main(Ex8_5.java:10)
```

### 멀티 catch블럭

내용이 같은 catch블럭을 하나로 합친 것(JDK1.7부터) (’|’ 를 사용해서, 합친다.)

예시

```java
try {
		...
} catch (ExceptionA e) {
	e.printStackTrace();
} catch (ExceptionB e2) {
	e2.printStackTrace();
}
```

같은 내용을 통일하고 중복을 제거하기 위해서는 아래와 같이 코드를 쓸 수 있다.

```java
try {
		...
} catch (ExceptionA | ExceptionB e) {
	e.printStackTrace();
} 
```

주의사항이 존재한다. 2가지 부모자식 관계일 경우에는 사용하지 않는다.

```java
try {
		...
// } catch (ParentExceptionA | ChildExceptionB e) { 부모자식관계일 경우에는 **ERROR**
} catch (ParentException e) { // OK. (조상타입으로 선언하면 되기 때문에)
	e.printStackTrace();
} 
```

참조멤버는 공통멤버만 사용가능하다.

```java
try {
		...
} catch (ParentExceptionA | ChildExceptionB e) {
		e.methodA(); // **ERROR** ExceptionA에 선언된 methodA()는 호출 불가 (공통멤버만 사용가능)
		
		**// 사용하고 싶을 때는**
		if(e instanceof ExceptionA) {
				ExceptionA e1 = **(ExceptionA)**e; // 형변환필요
				e1.methodA(); // OK. ExceptionA에 선언된 메서드 호출 가능
		} else { // if(e instanceof ExceptionB)
		...
		}
}
```