
# JSP 태그 
- JSP 코드 내에 JAVA 코드를 삽입 할 수 있게 해주는 태그를 의미

## Servlet 
- Java언어를 이용하여 문서를 작성하고 printWriter를 이용하여 HTML코드를 삽입

## JSP
- HTML 코드에 Java언어를 삽입하여 동적 문서를 작성함

- JSP는 HTML 기반의 웹 페이지이므로 동적 페이지로 만들려면 JSP 태그 사이에 Java 코드를 삽입해야 함
- JSP가 서블릿으로 변환된 후 사용자에게는 HTML 형태의 코드만 전송하므로 JSP 태그의 내용은 사용자에게 보여지지 않음

### 스크립트 태그
- 자바 코드를 JSP 내에서 활용하는데 도움을 주는 태그
- JSP 페이지가 서블릿 프로그램에서 서블릿 클래스로 변환될 때 JSP 컨테이너가 아래의 동작을 수행
	- 스크립트 태그를 처리해서 Java 코드를 사용
	- 나머지는 html, 일반 코드로 간주 함
### 선언문(declaration)

- 자바 변수나 메소드를 선언, 정의하는데 사용하는 태그
    
    ```JAVA
    <%@ page language="java" contentType="text/html; charset=EUC-KR"
       pageEncoding="EUC-KR"%>
    <!DOCTYPE html>
    <html>
    <head>
    <meta charset="EUC-KR">
    <title>scriptTag_test1</title>
    </head>
    <body>
    	<h2>script tag1</h2>
    	<%!
    		//내부는 전부 자바의 문법
    		//count는 전역변수
    		int count = 3;
    		String sayHello(String data){
    			return "Hello" + data;
    		}
    		//이곳은 서블릿 클래스의 영역이므로 소스코드를 작성할 수 없다.
    		//System.out.println();
    	%>
    </body>
    </html>
    ```
    
    내부에서 보통의 비즈니스 로직을 작성 할 수 없다지만 대신 메소드 내부에서 필요한 로직을 구현하면 된다.  
    또한 <%! %>의 내부에 작성한 코드는 서블릿 클래스에서 변수를 선언한 격으로 전역으로 선언된다.  
    위와 같이 선언한 메소드나 변수는 스크립트릿, 표현문에서 사용가능하다.

### [[디렉티브 태그]]
- JSP페이지 처리에 필요한 정보나 다른 JSP파일을 포함하고자 할 때 사용하는 태그
### [[액션 태그]]
- JSP 페이지 내에서 어떤 동작을 하도록 지시하는 태그

