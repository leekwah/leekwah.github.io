# page 디렉티브

## page 디렉티브

`page 디렉티브`는 JSP 페이지에 대한 정보를 입력하기 위해서 사용된다.<br>page 디렉티브를 사용하면 JSP 페이지가 어떤 문서를 생성하는지, 어떤 자바 클래스를 사용하는지, 세션(session)에 참여하는지, 출력 버퍼의 존재 여부와 같이 JSP 페이지를 실행하는 데 필요한 정보를 입력할 수 있다.

####  page 디렉티브의 예

```java
<%@ page contentType="text/html; charset=utf-8"%>
<%@ page import="java.util.Date"%>
```

두 개의 page 디렉티브를 보여주는데, 각각 contentType 속성과 import 속성을 사용하고 있다.<br>

#### page 디렉티브의 주요 속성

| 속성                           | 설명                                                         | 기본값    |
| ------------------------------ | ------------------------------------------------------------ | --------- |
| contentType                    | JSP가 생성할 문서의 MIME 타입과 캐릭터 인코딩을 지정한다.    | text/html |
| import                         | JSP 페이지에서 사용할 자바 클래스를 지정한다.                |           |
| session                        | JSP 페이지가 세션을 사용할지의 여부를 지정한다.<br>"true"를 사용할 경우 세션을 사용하고 "false"를 사용할 경우 세션을 사용하지 않는다. | true      |
| buffer                         | JSP 페이지의 출력 버퍼 크기를 지정한다.<br>"none"일 경우 출력 버퍼를 사용하지 않으며, "8kb"라고 입력한 경우 8킬로바이트 크기의 출력 버퍼를 사용한다. | 최소 8kb  |
| autoFlush                      | 출력 버퍼가 다 찼을 경우 자동으로 버퍼에 있는 데이터를 출력 스트림에 보이고 비울지 여부를 나타낸다.<br>"true"인 경우 버퍼의 내용을 웹 브라우저에 보낸 후 버퍼를 비우며, "false"인 경우 에러를 발생시킨다. | true      |
| info                           | jsp 페이지에 대한 설명을 입력한다.                           |           |
| errorPage                      | JSP 페이지를 실행하는 도중에 에러가 발생할 때 보여줄 페이지를 지정한다. |           |
| isErrorPage                    | 현재 페이지가 에러가 발생될 때 보여주는 페이지인가의 여부를 지정한다.<br>"true"일 경우 에러 페이지이며, "false"일 경우 에러 페이지가 아니다. | false     |
| pageEncoding                   | JSP 페이지 소스 코드의 캐릭터 인코딩을 지정한다.             |           |
| isELIgnored                    | "true"일 경우 표현 언어를 해석하지 않고 문자열로 처리하며, "false"일 경우 표현 언어를 지원한다. | false     |
| deferredSyntaxAllowedAsLiteral | #{ 문자가 문자열 값으로 사용되는 것을 허용할지의 여부를 지정한다. | false     |
| trimDirectiveWhitespaces       | 출력 결과에서 템플릿 텍스트의 공백 문자를 제거할지의 여부를 지정한다. | false     |

위의 표에서 표시한 속성 중에서 주로 사용하는 속성은 `contentType 속성`과 `import 속성`이다.<br>여기서는 `contentType 속성`과 `import 속성`과 함께 `trimDirectiveWhitespaces 속성`에 대해 알아볼 것이다.

## contentType 속성과 캐릭터 셋

page 디렉티브의 contentType 속성은 JSP 페이지가 생성할 `문서의 타입`을 지정한다.<br>contentType은 JSP가 생성할 문서의 MIME 타입을 입력한다.<br><u>JSP에서 주로 사용하는 MIME 타입은 "text/html"</u>이고 필요에 따라 "text/xml", "application/json" 등의 MIME 타입을 사용하기도 한다.<br>contentType 속성을 설정하지 않을 경우 기본 값은 ``"text/html"``이다.

#### contentType 속성의 값의 구성

```
TYPE

또는

TYPE; charset=캐릭터 셋
```

#### HTML 문서를 생성하는 경우 contentType 속성 설정 예

```java
<%@ page contentType="text/html" %>
```

> **MIME**
>
> `MIME(Multipurpose Internet Mail Extensions)`은 이메일의 내용을 설명하기 위해 정의되었다.<br>하지만, 메일뿐만 아니라 프로토콜에서도 응답 데이터의 내용을 설명하기 위해서 MIME을 사용하고 있다.

contentType 속성의 값 중에서 "; charset=캐릭터 셋" 부분은 생략할 수 있다.<br>캐릭터 셋 부분을 생략할 경우기본 캐릭터 셋인 `ISO-8859-1`을 사용하게 된다.<br>한글을 표현하려면 `EUC-KR`이나 `UTF-8`과 같이 한국어를 포함하고 있는 캐릭터 셋을 사용해야 한다. (기본 ISO-8859-1으로 한글 표현 불가능)

#### 캐릭터 셋 설정 예

```java
<%@ page contentType="text/html; charset=UTF-8"%>

또는

<%@ page contentType="text/html; charset=utf-8"%>
```

## import 속성

자바는 클래스의 완전한 이름 대신 단순한 이름을 사용하기 위해 `import 구문`을 사용한다.<br>이와 유사하게 JSP는 page 디렉티브의 import 속성을 사용해서 JSP 코드에서 클래스의 단순 이름을 사용할 수 있다.<br>import 속성의 값으로 여러 타입을 지정할 수도 있다.<br>이때 각 타입은 콤마로 구분한다.<br>패키지 이름 뒤에 별표(' \*')를 사용하면 해당 패키지에 속해 있는 모든 타입을 단순 이름으로 사용할 수 있다.<br>예를 들어, 아래 코드와 같이 import 속성의 값으로 "java.util.*"을 주면, JSP 코드에서 Date, Calendar 등 java.util 패키지에 속한 타입을 단순 타입으로 사용할 수 있다.

#### import 속성의 사용 예

```java
<%@ page import="java.util.Calendar" %>
<%@ page import="java.util.Date" %>
```

#### import 속성 값으로 여러 타입을 지정 예

```java
<%@ page import="java.util.Calendar, java.util.Date" %>
```

#### import 속성 값으로 패키지 지정 예

```java
<%@ page import="java.util.*" %>
```

> **클래스와 패키지 그리고 클래스의 이름**
>
> 클래스는 객체 지향 프로그래밍에서 사용하는 용어로서, 특별한 기능을 제공해주는 모듈이라고 생각하면 된다.<br>JSP 프로그래밍에서는 자바의 클래스를 사용해서 필요한 기능을 구현하게 된다.
> 패키지(package)는 이런 클래스들을 모아 놓은 단위다. 패키지의 이름은 [이름1].[이름2].[이름3]과 같이 점(.)으로 구분된 계층 구조를 갖는다.<br>
> 서로 다른 클래스에 같은 이름을 갖는 타입이 존재할 수 있다.<br>두 패키지에 속한 Date 타입은 서로 다른 타입이기 때문에 구분해서 표기할 수 있어야 하는데, 이때 사용되는 이름이 완전한 이름(Fully Qualified Name)이다.<br>패키지 이름을 제외한 나머지 부분은 단순 이름이라고 한다.<br>예를 들어, java.util.Date 타입의 단순 이름은 Date가 된다.

import의 속성값으로 "java.util.Calendar"를 설정하면 JSP는 단순 이름인 "Calendar"를 사용할 수 있다.<br>import 속성을 사용하지 않고 완전한 클래스 이름을 사용하여 클래스를 사용할 수도 있다.<br>import 속성을 사용하는 대신 java.util.Calendar를 사용해도 제대로 실행된다.

## trimDirectiveWhitespaces 속성을 이용한 공백 처리

```java
<%@ page contentType="text/html; charset=UTF-8" %>
<html>
<head>
<title>현재 시간</title>
</head>
<body>
지금 : <%= new java.util.Date() %>
</body>
</html>
```

위의 코드를 실행한 뒤 웹 브라우저에서 소스 보기를 해보면 다음 코드처럼 첫 줄에 빈 줄이 생성되는 것을 알 수 있다.<br>이 첫 줄의 공백은 다음의 page 디렉티브가 있던 위치에서 만들어진 것이다.

```java
<%@ page contentType="text/html; charset=UTF-8" %>
```

JSP 2.1 부터 page 디렉티브에 새롭게 추가된 `trimDirectiveWhitespaces` 속성을 사용하면 불필요하게 생성되는 줄바꿈 공백 문자를 제거할 수 있다.<br>trimDirectiveWhitespaces의 값을 true로 지정하면 디렉티브나 스크립트 코드 위치에서 발생하는 줄바꿈 공백 문자를 제거해준다.

```java
<%@ page contentType="text/html; charset=UTF-8" %>
<%@ page trimDirectiveWhitespaces="true" %>
<html>
<head>
<title>현재 시간</title>
</head>
<body>
지금 : <%= new java.util.Date() %>
</body>
</html>
```

아래의 응답 결과를 보면 디렉티브로 인해 발생한 공백 문자가 응답 결과에 포함되지 않는 것을 확인할 수 있다.

```java
<html>
<head>
<title>현재 시간</title>
</head>
<body>
지금 : Sun May 03 10:03:55 KST 2015
</body>
</html>
```

## JSP 페이지의 인코딩과 pageEncoding 속성

웹 컨테이너가 JSP 페이지를 읽어올 때 사용할 `캐릭터 셋을 결정하는 기본 과정`은 다음과 같다.

1. 파일이 `BOM`으로 시작하지 않을 경우
   A. 기본 인코딩을 이용해서 파일을 처음부터 읽고, `page 디렉티브의 pageEncoding 속성을 검색`한다.
   		(단, pageEncoding 속성을 찾기 이전에 ASCII 문자 이외의 글자가 포함되어 있지 않은 경우에만 적용된다.)
   B. pageEncoding 속성이 값을 갖고 있다면, 파일을 읽어올 때 속성 값을 캐릭터 셋으로 사용한다.
   C. pageEncoding 속성이 없다면, `contentType 속성을 검색`한다.
   		contentType 속성이 존재하고 charset을 이용해서 캐릭터 셋을 지정했다면, 파일을 읽어올 때 사용할 캐릭터 셋으로 charset에 지정한 값을 사용한다.
   		(단, contentType 속성을 찾기 이전에 ASCII 문자 이외의 글자가 포함되어 있지 않은 경우에만 적용된다.)
   D. 모두 해당되지 않을 경우 `ISO-8859-1`을 캐릭터 셋으로 사용한다.
2. 파일이 `BOM`으로 시작할 경우
   A. BOM을 이용해서 결정된 인코딩을 이용하여 파일을 읽고, page 디렉티브의 pageEncoding 속성을 검색한다.
   B. 만약 pageEncoding 속성의 값과 BOM을 이용해서 결정된 인코딩이 다르면 `에러를 발생`시킨다.

위 과정은 JSP 규약에 명시된 과정으로서, 웹 컨테이너는 위 과정을 최적화할 수도 있지만 기본 과정은 위와 비슷하다.<br>JSP 파일을 읽을 때는 page 디렉티브의 `pageEncoding 속성`과 `contentType 속성`을 사용해서 캐릭터 인코딩을 결정한다는 것을 알 수 있다.

> **BOM**
>
> BOM은 Byte Order Mark의 약자로 UTF-8, UTF-16, UTF-32와 같은 유니코드 인코딩에서 바이트의 순서가 리틀 앤디언(Little Endian)인지 빅 앤디언(Big Endian)인지 여부를 알려주는 16비트(2바이트) 값이다.

파일이 유니코드가 아니거나 파일이 BOM으로 시작하지 않을 경우, 먼저 pageEncoding 속성을 검색하고 그 다음에 contentType 속성의 charset의 값을 검색하게 된다.<br>따라서, pageEncoding을 지정하지 않은 상태에서 contentType 속성의 charset의 값을 잘못 지정하면 잘못된 인코딩을 이용해서 파일을 읽어오게 되며, 이는 <u>문자가 깨져서 출력되는 원인</u>이 된다.<br>pageEncoding 속성에 지정한 인코딩과 contentType 속성에 지정한 인코딩이 다를 수도 있다.<br><u>JSP 파일은 UTF-8로 작성하고 응답 결과는 EUC-KR로 생성하고 싶다면</u>, pageEncoding은 "UTF-8"로 지정하고 contentType 속성의 charset은 "EUC-KR"로 지정하면 된다.

#### pageEncoding 속성에 지정한 인코딩과 contentType 속성에 지정한 인코딩을 다르게 설정한 예

```java
<%@ page contentType="text/html; charset=EUC-KR" %>
<%@ page pageEncoding="UTF-8" %>
<%@ page import="java.util.Date() %>
<%
	Date now = new Date();
%>
<html>
<head>
<title>현재 시간</title>
</head>
<body>
현재 시간 : <%= now %>
</body>
</html>
```

웹 브라우저에서 위의 코드를 실행한 뒤 인코딩을 확인해보면 한국어(EUC-KR)임을 알 수 있다.