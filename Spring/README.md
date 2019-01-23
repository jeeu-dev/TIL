Spring
====================

> 자료 : 자바 스프링 프레임워크(ver.2018) – 신입 프로그래머를 위한 [강좌](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC_renew/)<br>
--------
> 2019-01-23
### 9. 의존객체 자동 주입
#### 9-1 : 의존 객체 자동 주입이란? <br>
→ 스프링 설정 파일에서 의존 객체를 주입할 때 <code>constructor-org</code> 또는 <code>property</code> 태그로 의존 대상 객체를 명시하지 않아도 스프링 컨테이너가 자동으로 필요한 의존 대상 객체를 찾아서 의존 대상 객체가 필요한 객체에 주입해 주는 기능이다. <br>
→ 구현 방법은 <code>@Autowired</code>와 <code>@Resource</code>어노테이션을 이용해서 쉽게 구현할 수 있다.

#### 9-2 : @Autowired <br>
→ 주입하려고 하는 <b>객체의 타입</b>이 일치하는 객체를 자동으로 주입한다.
→ "<b>타입</b>을 보고 <b>자동</b>으로 넣어준다" <br>

→ xml에 <code>bean</code>만 추가하고(따로 contructor-arg 명시 X class에서 <code>@Autowired</code>를 추가한다. <br>

→ 생성자의 Autowired를 쓸 때는 그냥 쓰면 됨. <br> 단, property나 method에 쓸 때는 반드시 default 생성자를 명시해줘야 함!
```java
#Default 생성자
pulic WordRegisterService(){

}

#property
@Autowired
private WordDao WordDao;

#method
@Autowired
public void setWordDao(WordDao wordDao){
	this.wordDao = wordDao;
}
```
#### 9-3 : @Resource <br>
→ 주입하려고 하는 <b>객체의 이름</b>이 일치하는 객체를 자동으로 주입한다.<br>
→ 생성자에는 쓰지 못한다. property 또는 method에만 쓸 수 있다. <br>
→ 마찬가지로 default 생성자를 명시해줘야 한다! <br>

### 10. 의존객체 선택
→ 다수의 빈(Bean) 객체 중 의존 객체의 대상이 되는 객체를 선택하는 방법에 대해서 학습 <br>
#### 10-1. 의존객체 선택 <br>
→ Exception : 동일한 객체가 2개 이상인 경우 스프링 컨테이너는 자동 주입 대상 객체를 판단하지 못해서 Exception을 발생시킨다. <br>
→ <code>qualifier</code>태그를 써준다.
```java
#Exception 발생
<bean id="wordDao1" class="com.word.dao.WordDao" />
<bean id="wordDao2" class="com.word.dao.WordDao" />
<bean id="wordDao3" class="com.word.dao.WordDao" />
```
→ 
```java
#.xml
<bean id="wordDao1" class="com.word.dao.WordDao">
  <qualifier value="userDao" />
</bean>

#.java
@Autowired
@Qualifier("UsedDao")
private WordDao wordDao;
```
→ but 아래의 경우는 가능하다. → 좋은 방법은 아니며, 추천하지 않음 : 코드가 길어지고 개발자가 혼동될 수 있음
```java
#.xml
<bean id="wordDao" class="com.word.dao.WordDao" />
<bean id="wordDao2" class="com.word.dao.WordDao" />
<bean id="wordDao3" class="com.word.dao.WordDao" />

#.java
@Autowired
private WordDao wordDao;
```
→ <code>qualifier</code>태그를 써라. <br>
#### 10-2. 의존객체 자동 주입 체크
→ 이렇게 하는건 초보들이나 하는거지 거의 하는 경우가 없음
- 빈(Bean) 객체가 없는데 Autowired를 썼을 경우 Exception이 발생하지 않게 하는 방법
→ Autowired의 속성 중 required라는 속성이 있는데 false로 두면 됨
```java
@Autowired(requred=false)
private WordDao wordDao;
```

#### 10-3. @Inject
→ @Autowired와 거의 비슷하게 @Inject 어노테이션을 이용해서 의존 객체를 자동으로 주입을 할 수 있다. @Autowired와 차이점이라면 @Autowired의 경우 required 속성을 이용해서 의존 대상 객체가 없어도 익셉션을 피할 수 있지만, Inject의 경우 required 속성을 지원하지 않는다. <br>
→ Q. 어느 것이 더 많이 쓰이나요? @Autowired vs @Inject <br>
→ A. @Autowired가 더 많이 쓰입니다. 정확하게 왜 더 많이 쓰이는지는 모르겠는데 실무에서 더 많이 씁니다. <br>
→ 댓글 : @Autowired - 스프링에서(만) 지원하는 어노테이션 / @Inject - 자바에서 지원하는 어노테이션 이라고 알고 있습니다 [링크](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC_renew/%EC%9D%98%EC%A1%B4%EA%B0%9D%EC%B2%B4-%EC%84%A0%ED%83%9D/) <br>
→ @Autowired의 qualifier처럼 @Inject는 @Named가 있음
```java
#.xml
<bean id="wordDao1" class="com.word.dao.WordDao" />

# .java
@Inject
@Named(value="wordDao1")
private WordDao wordDao;
```
- 많이 쓰이는 것 : @Autowired > @Resource > @Inject
- <code>qualifier</code>는 종종 쓰인다.
- <code>required</code>는 초짜 개발자,,들이 쓰지 않을까요?

음..

### 11. 생명주기(Life Cycle)
→ 스프링 컨테이너와 빈(Bean) 객체의 생명주기(Life Cycle)에 대해 학습.
#### 11-1 : 스프링 컨테이너 생명주기

```java
#생성 - GenericXmlApplicationContext를 이용한 스프링 컨테이너 초기화(생성)
GenericXmlApplicationContext ctx = new GenericXmlApplicationContext("classpath:appCtx.xml");
```
※ 스프링 컨테이너 생성과 빈 객체 생성 시점은 동일하다고 할 수 있다.

```java
#getBean()을 이용한 빈(Bean)객체 이용
BookRegisterService BookRegisterService = ctx.getBean("bookRegisterService", BookRegisterService.class);

BookSearchService BookSearchService = ctx.getBean("BookSearchService", BookSearchService.class);

MemberRegisterService memberRegisterService = ctx.getBean("memberRegisterService", MemberRegisterService.class);

MemeberSearchSerivce memberSearchService = ctx.getBean("memberSearchService", MemberSearchService.class);
```

```java
#소멸 - close()를 이용한 스프링 컨테이너 종료
ctx.close();
```
→ 스프링 컨테이너 소멸, 자동으로 빈 객체 소멸 <br>
→ 메모리에서 없어진다는 뜻 <br>


#### 11-2 : 빈(Bean)객체 생명주기
→ 빈(Bean)객체의 생명주기는 스프링 컨테이너의 생명주기와 같이 한다.
> 스프링 컨테이너 초기화 - 빈(Bean) 객체 생성 및 주입 <br>
> 스프링 컨테이너 종료 - 빈(Bean) 객체 소멸 <br>
- 빈(Bean) 객체 <br>
afterPropertiesSet() : 빈(Bean) 객체 생성시점에 호출 <br>
destroy() : 빈(Bean) 객체 소멸시점에 호출 <br>
→ 빈(Bean)객체의 생성시점과 소멸시점에 작업하고 싶으면 위의 메소드를 쓰면 됨 <br>
Ex) 인증 <br>

> 실습
```java
# appCtx.xml
 <context:annotation-config />

 <bean id="bookDao" class="com.brms.book.dao.BookDao" />
 <bean id="bookRegisterService" class="com.brms.book.service.BookRegisterService"/>
 <bean id="bookSearchService" class="com.brms.book.dao.BookSearchService" />
 <bean id="memberDao" class="com.brms.member.dao.MemberDao" />
 <bean id="memberRegisterService" class="com.brms.member.service.MemberRegisterService"/>
 <bean id="memberSearchService" class="com.brms.member.service.MemberSearchService" />

```
bookRegisterService가 스프링 컨테이너에 생성될 때 특정한 작업이 하고 싶다 <br> 
→ InitializingBean과 DisposableBean을 가지고 빈객체가 생성/소멸 될 때 특정한 작업 <br>
※ 특정한 작업 Ex) 아이디와 비밀번호를 가지고 DB 인증 절차 / 특정 네트워크 상에 있는 자원을 끌어온다 <br>
```java
public class bookRegisterService implements InitializingBean, DisposableBean{

	@Autowired
	private BookDao bookDao;

	public BookRegisterService(){}

	public void register(Book book){
		bookDao.insert(book);
	}

	@Override
	public void afterPropertiesSet() throws Exceoption{
		System.out.println("Bean 객체 생성");
	}

	@Override
	public void destroy() throws Exception{
		System.out.println("Bean 객체 소멸");
	}
}
```
#### 11-3 : init-method, destroy-method 속성
→ 빈(Bean) 객체를 생성할 때 속성값을 넣어줄 수 있다. <br>
```java
#.xml
<bean id="memberRegisterService" class="com.brms.member.service.MemberRegisterService" init-method="initMethod" destroy-method="destroyMethod" />
```
```java
#MemberRegisterService.java
public class MemberRegisterService{

	@Autowired
	private MemberDao memberDao;

	public MemberRegisterService(){ }

	public void register(Member member){
		memberDao.insert(member);
	}

	public void initMethod(){
		System.out.println(" -- initMethod() -- ");
	}

	public void destroyMethod(){
		System.out.println(" -- destroyMethod() -- ");
	}
}
```

--------
> 2019-01-22
### 6. DI(Dependency Injection)
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
### 7. 다양한 의존 객체 주입
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

- 7-4 : Map 타입 갭체 주입
- <code>Map</code> 태그 안에 <code>Key</code> 태그 - <code>Value</code> 태그 쌍으로 존재

### 8. 스프링 설정 파일 분리
- 스프링 설정 파일(xml)이 너무 많아지면 비효율적

- 8-1 : 스프링 설정파일 분리
> applicationContext.xml
>> appCtx1.xml / appCtx2.xml / appCtx3.xml <br>
→ 이런식으로 파일 분리
→ 기능별로 분리했기 때문에 기능별로 이름을 지어준다.
→ Ex) AppDaoService / AppDataBase / AppInformation / etc
→ 어차피 문자 형태이기 때문에 배열로 들어가게 할 수 있다. 배열 이용!
```java
String [] appCtxs = {"classpath:appCtx1.xml", "classpath:appCtx2.xml", "classpath:appCtx3.xml"};

GenericXmlApplicationContext ctx = new GenericXmlApplicationContext(appCtxs);
```
→ 하나의 xml 파일에서 다른 xml 파일을 <code>import</code> 시켜주면 불러올 때 <code>import</code>가 적힌 하나의 파일만 가져오면 된다!
```java
#하나의 xml 파일
<import resource="classpath:appCtx2.xml">
<import resource="classpath:appCtx3.xml">

<bean id= "~~~" class="~~~~">
 <constructor-arg ref="~~~"></constructor-arg>
</bean>
```
→ 이렇게 가져오는게 흔하지는 않음 / 그냥 배열로 가져오는 것을 더 선호


- 8-2 : Bean의 범위
- 클래스를 이용해서, new 키워드를 이용해서 객체를 생성할 때마다 메모리에 매번 새로운 객체가 생성됨 Ex) <code>new ClassName()</code>
- But 스프링에서는 xml을 통해 Container를 만들었고 그 Container 안에는 객체들이 생성되어 있음. 따라서 getBean을 쓸 때마다 개체를 생성하는 것이 아니라 '호출'하는 것. → 동일한 객체를 가르킬 수 있다는 것. 동일한 객체 참조<br>
→ 이것을 <code>싱글톤(Singleton)</code>이라고 한다. <br>
→ <code>싱글톤(Singleton)</code> <br>
: 스프링 컨테이너에서 생성된 빈(Bean)객체의 경우 동일한 타입에 대해서는 기본적으로 한 개만 생성되며, getBean() 메소드로 호출된 동일한 객체가 반환된다. ※ 강의 PPT 中 <br>
→ <code>프로토타입(Prototype)</code> <br>
: 싱글톤의 반대 개념. 프로톤타입의 경우 개발자는 별도로 설정을 해줘야 하는데, 스프링 설정 파일에서 빈(Bean)객체를 정의할 때 scope속성을 명시해 주면 된다. → 흔치 않음
```java
<bean id="dependencyBean" class="scope.ex.DependencyBean" scope="prototype">
 <constructor-arg ref="injectionBean" />
 <property name="injectionBean" ref="injectionBean" />
</bean>
```
- 싱글톤은 <code>Default</code> → 꼭 프로토타입으로 사용하겠다 할때만 scope에 명시



-------
> 2019-01-21
### 1. 스프링 개요
### 2. 개발 환경 구축
### 3. 스프링 프로젝트 생성 
<br/>: Maven을 이용해서 스프링 프로젝트를 생성하는 방법에 대하여 학습
- 프로젝트 생성
- pom.xml 작성
- 폴더 및 pom.xml 파일의 이해
: pom.xml 파일은 메이븐 설정 파일로 메이븐은 라이브러리를 연결해주고, 빌드를 위한 플랫폼이다. → 외부 레파지토리에서 내꺼로 다운로드 해준다
### 4. 처음해 보는 스프링 프로젝트
- dependency 태그→ 내가 필요한 모듈
- bulid 태그 → 빌드할 때 필요한 명령들
- Spring만이 가지고 있는 기능들
- 스프링컨테이너(ApplicationContext)의 객체 → bean(Object)
- 객체 생성 → 메모리에 로드되었다는 것 / ApplicationCOntext에 있다는 것은 New 키워드가 필요없음 → 객체 생성되어있음
### 5. 또 다른 프로젝트 생성방법
- 일일히 다 만드는 방법
- bean의 id는 고유한 id, class는 패키지 포함한 내용

### Next 6. DI(Dependency Injection)