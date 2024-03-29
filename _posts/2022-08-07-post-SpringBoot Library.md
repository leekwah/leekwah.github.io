---
title: SpringBoot Library
categories:
  - Develop
tags:
  - Spring
  - SpringBoot
---
## library

Gradle은 의존관계가 있는 라이브러리를 함께 다운로드 한다.

**스프링 부트 라이브러리**

- spring-boot-starter-web
  - **spring-boot-starter-tomcat : 톰캣 (웹서버) - 중요**
  - **spring-webmvc : 스프링 웹 MVC - 중요**
- spring-boot-starter-thymeleaf : 타임리프 템플릿 엔진(View)
- spring-boot-starter(공통) : 스프링 부트 + 스프링 코어 + 로깅
  - spring-boot
    - spring-core
  - spring-boot-starter-logging
    - logback, slf4j - 로깅을 할 때 최근에는 이렇게 쓴다.

**테스트 라이브러리**

- spring-boot-starter-test
  - junit : 테스트 프레임워크 (요새는 jnuit5를 많이 쓴다.)
  - mockito : 목 라이브러리
  - assertj : 테스트 코드를 좀 더 편하게 작성하게 도와주는 라이브러리
  - spring-test : 스프링 통합 테스트 지원