---
title: SELECT 명령
categories:
  - Develop
tags:
  - 오라클 SQL과 PL/SQL
  - ORACLE
  - SQL
---
## SELECT 명령어란?

SELECT 명령어는 데이터베이스에 저장되어 있는 데이터를 꺼내 와서 화면으로 보여달라는 뜻이다.<br>원하는 컬럼만 조회하기 위해서는 원하는 컬럼명을 적으면 된다.<br>컬럼이 여러개일 경우에는 ,(콤마)로 구분하고 이름을 여러개 적어 주면 된다.<br>전체 컬럼을 보고 싶을 경우에는 \*를 사용하면 된다.

```SQL
SELECT [필드] FROM [테이블];
```

## SELECT 명령에 표현식을 사용하여 출력하기

표현식(Expression)이란 컬럼 이름 이외에 출력하기를 원하는 내용을 의미하며 SELECT 구문 뒤에 \' \'(작은 따옴표)로 묶어서 사용하면 된다.

```SQL
SELECT [필드] 'HI' FROM [테이블];
```

위의 SQL문의 'HI'가 '표현식'이라고 하며, '리터럴(literal) 상수(문자)'라고도 부른다.

```SQL
SELECT DNAME, Q''', IT'S DEPTNO : ''' , DEPTNO "DNAME AND DEPTNO" FROM DEPT;
SELECT DNAME, Q'[, IT'S DEPTNO : ]' , DEPTNO "DNAME AND DEPTNO" FROM DEPT;
```

위의 SQL문에서 작은 따옴표가 리터럴 내에 있을 경우에는 작은따옴표 1개를 출력하기 위해서 2개를 사용해야한다. (또는 대괄호를 사용하는 방법도 있다.)

## 컬럼 별칭 사용하여 출력하기 - 컬럼별칭 (Column Alias)

```SQL
SELECT [필드] "별명" FROM [테이블];
SELECT [필드] AS 별명 FROM [테이블];
```

컬럼을 출력할 때 컬럼의 원래 이름 대신 별명을 사용할 수 있다.<br>테이블의 컬럼 이름이 변경된 것이 아니라, 출력될 때 임시로 바꾸어서 보여주는 것이다.<br>SQL문에 적혀있듯이 두 가지 방법으로 이용할 수 있다.<br>첫 번째 방법은 AS 라는 키워드를 사용한 후에 별명을 적는 것이고, 두 번째 방법은 \" \"(큰 따옴표)로 감싸주는 것이다.<br>기능상의 차이는 없으나, 별명에 공백이나 특수문자, 대소문자 구분이 필요할 경우에는 반드시 **"별명"**과 같은 형태로 써야한다.

## DISTINCT 명령어로 중복된 값을 제거하고 출력하기

```SQL
SELECT DISTINCT [필드] FROM [테이블];
```

데이터를 조회할 시에 중복된 데이터가 나오는 경우가 있는데, 이럴 때는 DISTINCT 키워드를 사용하면 된다.