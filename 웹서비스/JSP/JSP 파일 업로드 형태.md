# MultipartRequest

웹 페이지에서 서버로 업로드 되는 파일 자체만 다루는 클래스임

웹 브라우저가 전송한 multipart/form-data 유형과 POST 방식의 요청
파라미터 등을 분석한 후 일반 데이터와 파일 데이터를 구분하여 파일 데이터에 접근함

한글 인코딩 값을 얻기 쉽고, 서버의 파일 저장 폴더에 동일한 파일명이 있으면 파일명을 자동으로 변경함

```JSP
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>
<%@ page import="java.io.*, java.util.*, com.oreilly.servlet.*, com.oreilly.servlet.multipart.*" %>

<%
// 파일이 업로드될 경로 지정
String savePath = "파일을 저장할 경로를 입력하세요";

// 파일 업로드를 처리하기 위한 MultipartRequest 생성
MultipartRequest multi = new MultipartRequest(request, savePath, 10 * 1024 * 1024, "UTF-8");

// 업로드된 파일의 정보를 얻어옴
Enumeration files = multi.getFileNames();
while (files.hasMoreElements()) {
    String fileName = (String) files.nextElement();
    File file = multi.getFile(fileName);
    String originalFileName = multi.getOriginalFileName(fileName);
    String fileExtension = multi.getOriginalFileExtension(fileName);

    // 업로드된 파일 처리 로직 작성
    // 예를 들어, 파일을 저장하거나 데이터베이스에 파일 정보를 저장하는 등의 작업을 수행할 수 있습니다.
}
%>

```

위의 예제 코드는 com.oreilly.servlet 라이브러리를 사용하여 MultipartRequest를 생성하고, 업로드된 파일의 정보를 얻어오는 방법을 보여줍니다. 주석 부분에 업로드된 파일을 처리하는 로직을 추가하면 됩니다. 또한, `savePath` 변수에는 파일이 저장될 경로를 지정해주어야 합니다. 이 예제를 참고하여 파일 업로드 기능을 구현하시면 됩니다.