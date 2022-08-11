---
title: Object 클래스
categories:
  - Develop
tags:
  - Java
  - Chapter9
  - Object
  - 자바의 정석 기초편
---
## Object 클래스

모든 클래스의 최고조상으로 오직 11개의 메서드만을 가지고 있다.
notify()와 wait()는 쓰레드와 관련된 메서드이다.

![20220811_1](/assets/img/20220811_1.png)

finalize()는 마무리작업을 하는 것이지만, 메모리 정리하느라 시간이 많이 소요됨 -> 잘 사용하지 않게 됨
getClass()의 클래스정보는 설계도 정보이다.
Class에서 대문자는 클래스의 정보를 담귀위한 것이다.