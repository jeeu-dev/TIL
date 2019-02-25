Spring
====================

> 자료 : 실전 JSP (ver.2018) – 신입 프로그래머를 위한 [강좌](https://www.inflearn.com/course/%EC%8B%A4%EC%A0%84-jsp_renew/)<br>
-------
> 2019-02-13
### 1. 웹 프로그램 개요
#### 1-1 웹 프로그램이란?
#### 1-2 프로토콜(Protocal)과 IP
#### 1-3 웹프로그램의 동작 원리
<br>
### 2. 개발 환경 설정
#### 2-1 JDK 설치
#### 2-2 Path 설정
#### 2-3 이클립스 다운로드
#### 2-4 웹 컨테이너(Apache Tomcat 8.5) 설치

### 3. JSP 맛보기
#### 3-1 웹 컨테이너 구조
xxx.jsp → (Request) → 웹 컨테이너(tomcat) [xxx.java → xxx_java.class → xxx_jsp.obj] → (response) → HTML <br>
↑ 개발자는 여기까지만!

#### 3-2 JSP 파일 작성
`<%@ page language="java" conetentType="text/html; charset-EUC-KR" pageEncoding="EUC-KR" %>` <br>

#### 3-3 .java 파일 확인

### 4. Servlet 맛보기
#### 4-1 웹 컨테이너 구조
웹 컨테이너(tomcat) [xxx.java → xxx_java.class → xxx_jsp.obj] <br>

#### 4-2 Servlet 파일 작성

#### 4-3 .class 파일 확인

-------
> 2019-02-14
### 5. Servlet 맵핑
#### 5-1 Servlet 맴핑이란?
- Servlet 이름이 긴 것을 간결하고 보안에 취약하지도 않은 이름으로 바꾸는 것. <br>

#### 5-2 web.xml 파일을 이용한 맵핑
```xml
<servlet>
	<servlet-name>servletEx</servlet-name> <!-- 일종의 닉네임 -->
	<servlet-class>com.servlet.ServletEx</servlet-class> <!-- 실제 servlet -->
</servlet>
<servlet-mapping>
	<servlet-name>servletEx</servlet-name> 
	<url-pattern>/SE</url-pattern> <!-- mapping할 이름 -->
</servlet-mapping>

```

#### 5-3 java Annotation을 이용한 맵핑
```java
@webServlet("/Hello")
public class ServletEx extends HttpServlet{
	...
}
```

### 6. Servelt request, response
#### 6-1 HttpServlet
- 추상클래스라고 함(abstract class) <br>
- ServletEx(class) → HttpServlet(abstract class) → GenericServlet(abstract class) → Servlet(interface) <br>
																				  → ServletConfig(interface) <br>
																				  → Serializable(interface) <br>

```java
package com.servlet;

@webServlet("/SE")
public class ServletEx extends HttpServlet{

	protected void doGet(HttpservletRequest request, HttpServletResponse response) throws ServletException, IOException{

	}

	protected void doPost(HttpservletRequest request, HttpServletResponse response) throws ServletException, IOException{
		doGet(request, response);
	}
}

```
#### 6-2 HttpServletRequest
- 요청에 대한 정보를 가지고 있는 객체 <br>
request.getCookies(); <br>
request.getSession(); <br>
request.getAttribute(null); <br>
request.getParameter(null); <br>
request.getParameterNames(); <br>
request.getParameterValues(null); <br>
request.setAttribute(null, null); <br>
: 직관적으로 다 알 수 있을듯


#### 6-3 HttpServletResponse
- 응답에 대한 정보를 가지고 있는 객체 <br>
request.addCookie(null); <br>
request.getWriter(); <br>
request.getStatus(); <br>
request.getOutputStream(); <br>
request.sendRedirect(null); <br>

-------
> 2019-02-15

### 7. Servlet Life-Cycle
#### 7-1 Servlet 생명주기
- @PostConstruct → init() → service → destroy() → @PreDestroy (init ~ destroy : Servlet 생성 및 종료) <br>

#### 7-2 생명주기 관련 메서드
```java
@PostConstruct
public void funPc(){
	...
}

@Override
public void init() throws ServletExceoption{
	...
}

@Override
public void destroy(){
	...
}

@PreDestroy
public void funPd(){
	...
}
```

-------
> 2019-02-25

### 8. form 데이터 처리
→ 사용자의 form 데이터를 Servlet에서 처리하는 방법에 대해서 학습. <br>

#### 8-1 Form 태그
- Browser → Request(DATA) → 웹 컨테이너(tomcat) / servlet <br>

#### 8-2 doGet
- method="get" → doGet() <br>

#### 8-3 doPost
- method="post" → doPost() <br>

### 9. JSP 스크립트

#### 9-1 Servlet vs JSP
Servlet - JAVA 코드 / xxx.java → xxx.class <br>
JSP - HTML - JAVA 코드 / xxx.java → xxx_jsp.java → xxx_jsp.class <br>

#### 9-2 JSP파일 HTML5 포멧설정
Windows → Preference → Web → JSP Files → Editor → Templates → new → html 5 format 만들기 <br>

#### 9-3 JSP 주요 스크립트
- JSP페이지에서 Java의 멤버변수 또는 메서드를 선언 <br>
```html
<%!
 int num = 10;
 String str = "jsp";
 ArrayList<String> list = new ArrayList<String>();

 public void jspMethod(){
 	System.out.println("	jspMethod()	");
 }

%>
```
- jsp 주석은 jsp 파일이 서블릿 파일로 변환될 때 제외된다. <br>
```html
<!-- 주석 태그 -->
<%-- Hello JSP World! --%>
```
- 스크립트릿 태그 : JSP 페이지에서 Java 코드를 넣기 위한 태그
```html
<%
 if(num >0){
%>
<p> num > 0</p>
<%
 } else{
%>
<p> num <= 0 </p>
<%
 }
%>
```
- 표현식 태그 : Java의 변수 및 메서드의 반환값을 출력하는 태그
```
 num is <%= num %>
```
- 지시어 : 서버에서 jsp 페이지를 처리하는 방법에 대한 정의
1) page : 페이지 기본 설정 → <% page 속성 = "속성 값">
```
<%@ page language="java" contentType="text/html; charset-EUC-KR" pageEncoding="EUC-KR"%>
```
2) include : include file 설정 → <% include file="파일명">
```
<%@ include file="header.jsp"%>
```
3) taglib : 외부라이브러리 태그 설정 → <% taglib uri="uri" prefix="네임스페이스명">
```
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
```

### 10. JSP request, response

#### 10-1 request 객체


#### 10-2 response 객체


