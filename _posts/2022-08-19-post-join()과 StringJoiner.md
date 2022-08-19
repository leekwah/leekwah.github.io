---
title: join()과 StringJoiner
categories:
  - Develop
tags:
  - Java
  - 자바의 정석 기초편
---
# join()과 StringJoiner

join()은 (static메서드)  여러 문자열 사이에 구분자를 넣어서 결합한다.

```Java
String animals = "dog, cat, bear";
String[] arr = animals.split(",");  // split으로 ","을 기준으로 자른 것이 array에 저장된다.
String str = String.join("-", arr); // 배열의 문자열을 '-'로 구분해서 결합한다.
System.out.println(str); // "dog-cat-bear" 이 출력된다.
```

