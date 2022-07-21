---
title: Javascript Basic
categories:
  - Post Formats
tags:
  - JavaScript
  - 연산자
---
<h3>변수</h3>

변수는 데이터를 담을 수 있는 <span style="color:gold">그릇</span>이다.
<span style="background-color:blue; color:white;">기본형 | var 변수명; 또는 var 변수명 = 값;<sapn>

<h3>연산자</h3>

|종 류|기본형|설명|
|:---:|:---:|:---:|
|\+|A \+ B|더하기|
|\-|A \- B|빼기|
|\*|A \* B|곱하기|
|\/|A \/ B|나누기|
|\%|A \= A \% B|나머지|  
```javascript
    var num1 = 15;
    var num2 = 2;
    var result;

    result = num1 + num2;
    document.write(result,"<br>");
    result = num1 - num2;
    document.write(result,"<br>");
    result = num1 * num2;
    document.write(result,"<br>");
    result = num1 / num2;
    document.write(result,"<br>");
    result = num1 % num2;
    document.write(result,"<br>");
```
```javascript
    var str = "<table border='1'>";
    str += "<tr>";
    str += "<td>1</td><td>2</td><td>3</td>";
    str += "</tr>";
    str += "</table>";

    document.write(str);
```

<h3>대입연산자</h3>

|종 류|풀 이|
|:---:|:---:|
|A \= B|A \= B|
|A \+\= B|A \= A \+ B|
|A \-\= B|A \= A \- B|
|A \*\= B|A \= A \* B|
|A \%\= B|A \= A \% B|
<br>

```javascript
    var num1 = 10;
    var num2 = 3;
    num1 += num2 // num1 = 10 + 3
    document.write(num1,"<br>"); // 13이 출력된다.

    num1 -= num2 // num1 = num1 - num2 => 앞에 있던 값(13)으로 빼기에 13 - 3 = 10
    document.write(num1,"<br>"); // 10이 출력된다.

    num1 *= num2 // num1 = num1 * num2 => 10 * 3 = 30
    document.write(num1,"<br>"); // 30이 출력된다.

    num1 %= num2 // num1 = num1 / num2 => 30 * 3 = 10 ... 0 나머지 0
    document.write(num1,"<br>"); // 0이 출력된다. num1 /= num2 였다면, 10이 출력됐을 것이다.
```
<h3>증감연산자</h3>  
  
<span style="color:gold;">기본형 | var 변수명; 또는 var 변수명 = 값;<sapn>