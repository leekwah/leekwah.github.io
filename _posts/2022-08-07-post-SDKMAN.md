---
title: SDKMAN
categories:
  - Develop
tags:
  - Java
  - MacOS
---
# SDKMAN

## MacOS에서는 SDKMAN을 통해서, Java의 버전을 관리할 수 있다.

```terminal
$ sdk version // sdkman 버전출력
$ sdk version //sdkman 버전출력  
$ sdk list java // 설치 가능, 설치된 JDK목록  
$ sdk install java 11.0.16-amzn // 지정된 JDK설치 (11.0.16-amzn을 설치한다.)
$ sdk default java 11.0.16-amzn // 사용할 java버전을 변경 (모든 쉘에 적용한다.)
$ sdk use java 11.0.16-amzn // 어떤 java버전을 사용할 것인지, 지정 후 사용한다.
$ sdk current java // 현재 사용중인 java버전 출력한다.
$ echo $JAVA_HOME // JAVA_HOME으로 지정된 경로를 출력한다.
```