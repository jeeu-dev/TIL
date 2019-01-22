Spring
====================

> 자료 : 자바 스프링 프레임워크(ver.2018) – 신입 프로그래머를 위한 [강좌](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC_renew/)<br>
-------

> 2019-01-22
#### 6. DI(Dependency Injection)
- Spring 설정 파일(ApplicationContext)를 통해서 객체 생성
- DI(의존성 주입)란? <br>
EX)
- 배터리 일체형 → 배터리 교체 불가(장난감 새로 구입) <br>
- 배터리 분리형 → 배터리만 교체하면 됨 <br>
- 스프링 컨테이너 생성 및 빈(Bean) 객체 호출 과정 <br>
→ 스프링 설정파일(ApplicationContext.xml)을 통해 Spring Container 생성<br>
→ Spring Container 안에 객체가 있고 객체 안에 또 객체가 있을 수 있음 <br>
→ 의존성 주입 방식 → 생성자 방식 / Setter 방식 <br> 
- DAO를 통해 DB와 통신
- DAO 생성 후 모든 객체에 DAO 주입
- 스프링에서는 'new 생성자' 하지않고 ApplicationContext에서 bean 태그에서 constructor-arg 등록한 다음, 주입할 dao를 ref로 넣는다.
- GenericXmlApplicationContext & getBean 사용
#### 7. 다양한 의존 객체 주입
- 7-1 : 생성자를 이용한 의존 객체 주입 <br>
```java
public StudentRegisterService(StudentDao studentDao){
	this.studentDao = studentDao;
}
```

→ <br>
```java
<bean id="studentDao" class="ems.member.dao.StudentDao"></bean>
<bean id="registerService" class="ems.member.service.StudentRegisterService">
	<constructor-arg ref="studentDao"></constructor-arg>
</bean>
```

- 7-2 : setter를 이용한 의존 객체 주입
- set을 띄고 첫번째 글자를 소문자로 바꿔서 property name에 표현(규칙임), parameter로 들어오는 값들을 value에 속성 값으로 이용할 수 있음

```java
public void setJdbcUrl(String setJdbcUrl){
	this.jdbcUrl = jdbcUrl;
}
```
→
```java
<bean id="dataBaseConnectionInfoDev" class="ems.member.dataBaseConnectionInfoDev">
 <property name = "jdbcUrl" value="jdbc:oracl:this:@localhost:1521:xe"/>
</bean>
```

- 7-3 : List 타입 의존 객체 주입
- list의 경우 <code>list</code> 태그를 써서 value를 주입한다.
```java
<property name="developers">
 <list>
   <value>Cheney.</value>
   <value>Eloy.</value>
   <value>Jasper.</value>
   <value>Kian.</value>
</property>
```











-------
> 2019-01-21
#### 1. 스프링 개요
#### 2. 개발 환경 구축
#### 3. 스프링 프로젝트 생성 
<br/>: Maven을 이용해서 스프링 프로젝트를 생성하는 방법에 대하여 학습
- 프로젝트 생성
- pom.xml 작성
- 폴더 및 pom.xml 파일의 이해
: pom.xml 파일은 메이븐 설정 파일로 메이븐은 라이브러리를 연결해주고, 빌드를 위한 플랫폼이다. → 외부 레파지토리에서 내꺼로 다운로드 해준다
#### 4. 처음해 보는 스프링 프로젝트
- dependency 태그→ 내가 필요한 모듈
- bulid 태그 → 빌드할 때 필요한 명령들
- Spring만이 가지고 있는 기능들
- 스프링컨테이너(ApplicationContext)의 객체 → bean(Object)
- 객체 생성 → 메모리에 로드되었다는 것 / ApplicationCOntext에 있다는 것은 New 키워드가 필요없음 → 객체 생성되어있음
#### 5. 또 다른 프로젝트 생성방법
- 일일히 다 만드는 방법
- bean의 id는 고유한 id, class는 패키지 포함한 내용

#### Next 6. DI(Dependency Injection)