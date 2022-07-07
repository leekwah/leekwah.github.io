---
title: 대입연산자
comments: null
read_time: true
layout: tags
author_profile: true
tag: 
- JavaScript
- THU
---
대입연산자
---
|종 류|풀 이|
|:---:|:---:|
|A \= B|A \= B|
|A \+\= B|A \= A \+ B|
|A \-\= B|A \= A \- B|
|A \*\= B|A \= A \* B|
|A \%\= B|A \= A \% B|

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