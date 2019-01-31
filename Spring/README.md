Spring
====================

> 자료 : 자바 스프링 프레임워크(ver.2018) – 신입 프로그래머를 위한 [강좌](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC_renew/)<br>
--------
> 2019-02-01
### 21. 리다이렉트, 인터셉트
#### 21-1 리다이렉트(Redirect)


#### 21-2 인터셉터(Interceptor)






--------
> 2019-01-30
### 19. Controller 객체 구현 - 2
#### 19-1 @ModelAttribute
- @ModelAttribute를 이용하면 커멘드 객체의 이름을 변경할 수 있고, 이렇게 변경된 이름은 뷰에서 커멘드 객체를 참조할 때 사용된다. 
```java
//컨트롤러

public String memberJoin(Member member)
```
↓
```jsp
//memJoinOk.jsp
ID : ${member.memId}
```
- @ModelAttribute를 이용하여 값을 바로 뷰에서 이용할 수 있다.
```java
//.java
@ModelAttribute("serverTime")
public String getServerTime(Locale locale){
```
↓
```jsp
//.jsp
<p> The time on the server is ${serverTime}. </p>
```

- 공통 데이터, 공통 메소드를 정할 수 있다.
```java
// 컨트롤러
public String memRemove(@ModelAttribute("mem") Member memeber)
```
↓
```jsp
//.jsp
ID : ${mem.memId}
```

#### 19-2 커맨드 객체 프로퍼티 데이터 타입
- 데이터가 기초데이터 타입인 경우
```html
//memberJoin.html
ID : <input type="text" name="memId">
PW : <input type="password" name="memPw">
MAIL : <input type="text" name="memMail">
AGE : <input type="text" name="memAge" size="4" value="0">
```
↓
```java
//Member.java
private String memId;
private String memPw;
private String memMail;
private int memAge;
```
- 데이터가 중첩 커멘드 객체를 이용한 List 구조인 경우
```html
<!-- memberJoin.html -->
PHONE1 : <input type="text" name="memPhones[0].memPhone1" size="5"> - <input type="text" name="memPhones[0].memPhone2" size="5"> - <input type="text" name="memPhones[0].memPhone3" size="5">
PHONE2 : <input type="text" name="memPhones[1].memPhone1" size="5"> - <input type="text" name="memPhones[1].memPhone2" size="5"> - <input type="text" name="memPhones[1].memPhone3" size="5">
```
↓
```java
//Member.java
private List<MemPhone> memPhones;
```

#### 19-3 Model & ModelAndView
- 컨트롤러에서 뷰에 데이터를 전달하기 위해 사용되는 객체로 Model과 ModelAndView가 있다. 두 객체의 차이점은 Model은 <b>뷰에 데이터만</b>을 전달하기 위한 객체이고, ModelAndView는 <b>데이터와 뷰의 이름을 함께 전달</b>하는 객체이다. 
- Model
```java
@RequestMapping(value="/memModify", method=RequestMethod.POST)
public String memModify(Model model, Member member){

	Member[] members = service.memberModify(member);

	model.addAttribute("memBef", members[0]);
	model.addAttribute("memAff", members[1]);

	return "memModifyOk";
}
```
↓ 뷰에 데이터만 전달
```html
<!-- memMofifyOk.jsp -->
ID : ${memBef.memId}
ID : ${memAff.memId}
```
- ModelAndView
```java
@RequestMapping(value="/memModify", method=RequestMethod.POST)
public String memModify(Model model, Member member){

	Member[] members = service.memberModify(member);

	model.addAttribute("memBef", members[0]);
	model.addAttribute("memAff", members[1]);

	return "memModifyOk";
}
```
↓ 아래와 같이 바뀌어야 한다.
```java
@RequestMapping(value="/memModify", method=RequestMethod.POST)
public ModelAndView memModify(Member member){ // 데이터 타입 : ModelAndView

	Member[] members = service.memberModify(member);

	ModelAndView mav = new ModelAndView(); //ModelAndView 객체 생성
	model.addAttribute("memBef", members[0]);
	model.addAttribute("memAff", members[1]);

	mav.setViewName("memModifyOk"); // 뷰의 이름을 set

	return mav; // ModelAndView 객체(모델이름을 같이) 반환
}
```

### 20. 세션, 쿠키
→ 클라이언트와 서버의 연결을 유지하는 방법
#### 20-1 세션(Session)과 쿠키(Cookie)
- Connectionless Protocol <br>
: 웹서비스는 HTTP 프로토콜을 기반으로 하는데, HTTP 프로토콜은 클라이언트와 서버의 관계를 <b>유지하지 않는</b> 특징이 있다. <br>
클라이언트 → 1. 요청(Request) : 서버 연결 → 서버 <br>
서버 → 2. 응답(Response) : 서버 연결 해제 → 클라이언트 <br>
- 서버의 부하를 줄일 수 있는 장점은 있나, 클라이언트트의 요청 시마다 서버와 매번 새로운 연결이 생성되기 때문에 일반적인 로그인 상태 유지, 장바구니 등의 기능을 구현하기 어렵다. <br>
클라이언트 → 1. 로그인 요청 → 서버 <br>
서버 → 2. 로그인 성공 응답 → 클라이언트 <br>
클라이언트 → 3. 상품 주문 요청 → 서버 <br>
서버 → 4. 로그인 유도 페이지 응답 → 클라이언트 <br>
- 이러한 Connectionless Protocol의 불편함을 해결하기 위해서 세션과 쿠키를 이용한다.
- 세션과 쿠키는 클라이언트와 서버의 연결 상태를 유지해주는 방법으로, 세션은 <b>서버에서 연결 정보를 관리</b>하는 반면 쿠키는 <b>클라이언트에서 연결 정보를 관리</b>하는데 차이가 있다.

#### 20-2 HttpServletRequest를 이용한 세션 사용
- 예제 : lec20Pjt001
클라이언트 → 1-1. 회원가입 요청 → 서버 <br>
서버 → 1-2. 회원가입 응답 → 클라이언트 <br>
클라이언트 → 2-1. 로그인 요청 → 서버 <br>
서버 → 2-2. 로그인 응답 : 세션 생성 → 세션 생성 <br>
클라이언트 → 3-1. 회원정보 수정 요청 → 서버 <br>
서버 → 3-2. 회원정보 수정 응답 : 세션 이용 → 세션 생성 <br>
클라이언트 → 4-1. 회원정보 삭제 요청 → 서버 <br>
서버 → 3-2. 회원정보 수정 응답 : 세션 이용 → 세션 생성 <br>

- 스프링 MVC에서 HttpServletRequest를 이용해서 세션을 이용하려면 컨트롤러의 메소드에서 파라미터로 HttpServletRequest를 받으면 된다.
```java
@RequestMapping(value="/login", method=RequestMethod.POST)
public String memLogin(Member member, HttpServletRequest request){

	Member mem = service.memberSearch(member);

	HttpSession session = request.getSession(); // 세션을 생성했다, 엄밀히 말하면 세션을 추가했다 라고 한다.
	session.setAttribute("member", mem);

	return "/member/loginOk";
}
```

#### 20-3 HttpSession을 이용한 세션 사용
- HttpServletRequest와 HttpSession의 차이점은 거의 없으며, 단지 세션객체를 얻는 방법에 차이가 있을 뿐이다. <br>
HttpServletRequest : 파라미터로 HttpServletRequest를 받은 후 getSession()으로 세션 얻음. <br>
HttpSession : 파라미터로 HttpSession을 받아 세션 사용. <br>
```java
public String memLogin(Member member, HttpServletRequest request){
	...
	HttpSession session = request.getSession();
	session.setAtrribute("member", mem);
	...
}
```
```java
public String memLogin(Member member, HttpSession session){
	...
	session.setAttribute("member", mem);
	...
}
```

#### 20-4 세션 삭제
- 세션을 삭제하는 방법은 세션에 저장된 속성이 더 이상 필요 없을 때 이루어지는 과정으로 주로 <b>로그아웃</b> 또는 <b>회원 탈퇴</b> 등에 사용된다. <br>
```java
// 로그아웃
public String memLogout(Member member, HttpServletRequest request){

	HttpSession session = request.getSession();
	session.invalidate(); // invalidate하면 삭제 된다.

	return "/member/logoutOk";
}
```
```java
// 회원 삭제 
public String memRemove(Member member, HttpServletRequest request){

	service.memberRemove(member);

	HttpSession session = request.getSession();
	session.invalidate(); // invalidate하면 삭제 된다.

	return "/member/removeOk";
}
```

#### 20-5 세션 주요 메소드 및 플로어
 세션 메소드 | 기능 
 :---:| :---:
 getId() | 세션 ID를 반환한다.
 setAttribute() | 세션 객체에 속성을 저장한다.
 getAttribute() | 세션 객체에 저장된 속성을 반환한다.
 removeAttribute() | 세션 객체에 저장된 속성을 제거한다.
 setMaxInactiveInterval() | 세션 객체의 유지시간을 설정한다.
 getMaxInactiveInterval() | 세션 객체의 유지시간을 반환한다.
 invalidate() | 세션 객체의 모든 정보를 삭제한다.

클라이언트 1. 서버 연결 및 요청 → 서버 2. setAttribute("member", mem) <br>
세션 3. member 속성 저장 → 클라이언트 4. 응답 <br>
클라이언트 5. 요청 → 서버 6. getAttribute("member") → 세션 7. member 속성 반환 → 클라이언트 8. 응답 <br>

#### 20-6 쿠키(Cookie)
- 세션과 쿠키는 동일하다 - 서버와 클라이언트의 연결을 유지시켜준다. but 쿠키는 클라이언트 즉, 사용자의 로컬 컴퓨터에 정보가 남아있게 된다.
- 예제 : lec20Pjt002
 - mallMain()에서 쿠키를 생성하고, 파라미터로 받은 HttpServletResponse에 쿠키를 담고 있다.
 - 쿠키를 생성할 때는 생성자에 두 개의 파라미터를 넣어주는데 첫 번째는 쿠키이름을 넣어주고 두 번째는 쿠키값을 넣어 준다.

 ```java
 @RequestMapping("/main")
 public String mallMain(Mall mall, HttpServletResponse response){

 	Cookie genderCookie = new Cookie("gender", mall.getGender());

 	if(mall.isCookieDel()){
 		genderCookie.setMaxAge(0);
 		mall.setGender(null);
 	}else{
 		genderCookie.setMaxAge(60*60*24*30); // 유지해라
 	}
 	 response.addCookie(genderCookie);

 	 return "/mall/main";
 }
 ```

- 예제 : lec20Pjt002
 - mallMain()에서 생성된 쿠키를 mallIndex()에서 사용한다.
 - 쿠키를 사용할 때는 @CookieValue를 사용한다.

 ```java
 @RequestMapping("/index")
 public String mallIndex(Mall mall,
 	@CookieValue(value="gender", required=false) Cookie genderCookie, //value는 쿠키의 이름, required는 찾는 이름이 없으면 익셉션이 발생하는데, 없더라도 '익셉션이 발생하지 마라' 라고 하기 위해 false로 설정함
 	HttpServletRequest request){

 	if(genderCookie != null)
 		mall.setGender(genderCookie.getValue());

 	return "/mall/index";
 }
 ```
- `@CookieValue`어노테이션의 value 속성은 쿠키 이름을 나타내는데, 만약 value에 명시한 쿠키가 없을 경우 익셉션이 발생한다. <br> 익셉션을 막는 방법이 있는데, 바로 required 속성이다. Required 속성은 기본값으로 true를 가지고 있는데 required가 true인 경우 value값에 해당하는 쿠키가 없으면 익셉션이 발생한다. <br> 따라서 requried 속성값을 false로 설정해서 value값에 해당하는 쿠키가 없어도 익셉션이 발생하지 않도록 한다.


--------
> 2019-01-29
### 16. STS를 이용하지 않은 웹 프로젝트
#### 16-1 스프링 MVC 웹 애플리케이션 제작을 위한 폴더 생성
C:\spinrg\pjt\lec16Pjt001\sec
C:\spinrg\pjt\lec16Pjt001\sec\main
C:\spinrg\pjt\lec16Pjt001\sec\main\java
C:\spinrg\pjt\lec16Pjt001\sec\main\webapp
C:\spinrg\pjt\lec16Pjt001\sec\main\webapp\resources
C:\spinrg\pjt\lec16Pjt001\sec\main\webapp\WEB-INF
C:\spinrg\pjt\lec16Pjt001\sec\main\webapp\WEB-INF\spring
C:\spinrg\pjt\lec16Pjt001\sec\main\webapp\WEB-INF\views

#### 16-2 pom.xml 및 이클립스 import

#### 16-3 web.xml 작성

#### 16-4 스프링 설정 파일(servlet-context.xml) 작성
/WEB-INF/spinrg/appServlet/servlet-context.xml

#### 16-5 root-context.xml 작성

#### 16-6 컨트롤러와 뷰 작성
```java
@Controller
public class HomeController{

	@RequestMapping("/")
	public String home(Model model){

		System.out.println("--- home() method ---")''

		model.addAttribute("key", "home value");

		return "home";
	}

	@RequestMapping("/login")
	public String login(Model model){

		System.out.println("--- login() method ---")''

		model.addAttribute("key", "login value");

		return "login";
	}
}
```

```html
<html>
<head>
	<title>Home</title>
</head>
<body>
<h1>
	Hello world! <br>
	key is${key}
</h1>
</body>
</html>
```
```html
<html>
<head>
	<title>Login</title>
</head>
<body>
<h1>
	Hello world! <br>
	key is${key}
</h1>
</body>
</html>
```

#### 16-7 실행

### 17. Service & Dao 객체 구현
#### 17-1 웹 어플리케이션 준비
<b>사용자요청(브라우저) → 프론트 컨트롤러(DispatcherServlet)(←→뷰(jsp파일)) → 컨트롤러 → 서비스 → DAO(Data Access Object) → Database </b>

#### 17-2 한글 처리
```xml
<!-- web.xml -->
<filter>
  <filter-name>encodingFilter</filter-name>
  <filter-Class>
    org.springframework.web.filter.CharacterEncodingFilter
  </filter-Class>
  <init-param>
    <param-name>encoding</param-name>
    <param-value>UTF-8</param-value>
  </init-param>
  <init-param>
    <param-name>forceEncoding</param-name>
    <param-value>true</param-value>
  </init-param>
</filter>

<filter-mapping>
  <filter-name>encodingFilter</filter-name>
  <url-pattern>/*</url-pattern>
</filter-mapping>

```
→ 프로젝트 할 때 딱 한번만 쓰니까 재활용하자~

#### 17-3 서비스 객체 구현
- 방법 1 : new 연산자를 이요한 service 객체 생성 및 참조
```java
MemberService service = new MemberService();
```
- 방법 2 : 스프링 설정 파일을 이용한 서비스 객체 생성 및 의존 객체 자동 주입
```java
<beans:bean id="service" class="com.bs.lec17.member.service.MemberService"></beans:bean>
```
↓
```java
@Autowired
MemberService service;
```
- 방법 3 : 어노테이션을 이용해서 서비스 객체 생성 및 의존 객체 자동 주입 / <code>@Service</code>, <code>@Component</code>, <code>@Repository</code> 중 어느 것을 써도 무방함
```java
@Repository("memService")
public class MemberService implements IMemberService(){
```
↓
```java
@Resource(name="memService")
MemberService service;
```

#### 17-4 DAO 객체 구현
- 방법 : 어노테이션을 이용해서 DAO 객체 생성 및 의존 객체 자동 주입
```java
@Repository
public class MemberDao implements IMemeberDao{
```
↓
```java
@Autowired
MemberDao dao;
```

### 18. Controller 객체 구현
#### 18-1 웹 어플리케이션 준비
- src/main/java <br>
컨트롤러 객체 <br>
DAO(Data Access Object) <br>
서비스 객체
- src/main/webapp/resources/html <br>
웹 컴포넌트
- ../WEB-INF/views
뷰(JSP) 컴포넌트 <br>

#### 18-2 @RequestMapping을 이용한 URL 맵핑
```java
@Controller
@RequestMapping("/member") 
public class MemberController{
	@Resource(name="memService")
	MemberService service;

	@RequestMapping(value="/memJoin", method=RequestMethod.POST)
	public String memJoin(Model model, HttpServletRequest request){
		String memId = request.getParameter("memId");
		String memPw = request.getParameter("memPw");
		String memMail = request.getParameter("memMail");
		String memPhone1 = request.getParameter("memPhone1");
		String memPhone2 = request.getParameter("memPhone2");
		String memPhone3 = request.getParameter("memPhone3");

		service.memberRegister(memId, memPw, memMail, memPhone1, memPhone2, memPhone3);

		model.addAttribute("memId", memId);
		model.addAttribute("memPw", memPw);
		model.addAttribute("memMail", memMail);
		model.addAttribute("memPhone", memPhone1 + "-" + memPhone2 + "-" + memPhone3);

		return "memJoinOk";
	}
}

```

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h1>Member Join</h1>
	<form action="/lec17/memJoin" method="post">
		ID : <input type="text" name="memId" ><br />
		PW : <input type="password" name="memPw" ><br />
		MAIL : <input type="password" name="memMail" ><br />
		PHONE : <input type="text" name="memPhone1" size="5"> - 
				<input type="text" name="memPhone2" size="5"> - 
				<input type="text" name="memPhone3" size="5"><br />
		<input type="submit" value="Join">
		<input type="reset" value="Cancel">
	</form>
	<a href="/lec17/resources/html/login.html">LOGIN</a> &nbsp;&nbsp; <a href="/lec17/resources/html/memjoin.html">JOIN</a>
</html>
```

#### 18-3 요청 파라미터
- HttpServletRequest 객체를 이용한 HTTP 전송 정보 얻기 
```html
ID : <input type="text" name="memId">
```
```java
	@RequestMapping(value="/memLogin", method=RequestMethod.POST)
	public String memLogin(Model model, HttpServletRequest request){  // 추가된 곳 

	String memId = request.getParameter("memId");
```
- @RequestParam 어노테이션을 이용한 HTTP 전송 정보 얻기
```html
ID : <input type="text" name="memId">
PW : <input type="password" name="memPw">
```
```java
	@RequestMapping(value="/memLogin", method=RequestMethod.POST)
	public String memLogin(Model model, @RequestParam("memId") String memId, @RequestParam("memPw") String memPw){  // 추가된 곳 
		//@RequestParam(value="memPw", required=false, defautValue="1234") // 이 속성도 이용할 수 있다 // 잘 사용안함

		// String memId = request.getParameter("memId");
		// String memPw = request.getParameter("memPw");
 
		Member member = service.memberSearch(memId, memPw);

		try{
			model.addAttribute("memId", member.getMemId());
			model.addAttribute("memPw", member.getMemPw());
		} catch (Exception e){
			e.printStackTrace();
		}

		return "memLoginOk";
	}
```
- 커멘드 객체를 이용한 HTTP 전송 정보 얻기 
<b>→ 가장 대중적</b>
```html
//memJoin.html
ID : <input type="text" name="memId"> <br />
PW : <input type="password" name="memPw"> <br />
MAIL : <input type="text" name="memMail"> <br />
```
```java
//Member.java
	public void setMemId(String memId){
		this.memId = memId;
	}

	public void setMemPw(String memPw){
		this.memPw = memPw;
	}

	public void setMemMail(String memMail){
		this.memMail = memMail;
	}
```

```java
//Controller.java
	@RequestMapping(value="/memJon", method=RequestMethod.POST)
	public String memJoin(Member member){
		...
	}
```
↓ 이렇게
```java
@Controller
@RequestMapping("/member") 
public class MemberController{
	@Resource(name="memService")
	MemberService service;

	@RequestMapping(value="/memJoin", method=RequestMethod.POST)
	public String memJoin(Member member){
		// String memId = request.getParameter("memId");
		// String memPw = request.getParameter("memPw");
		// String memMail = request.getParameter("memMail");
		// String memPhone1 = request.getParameter("memPhone1");
		// String memPhone2 = request.getParameter("memPhone2");
		// String memPhone3 = request.getParameter("memPhone3");

		service.memberRegister(member.getMemId(), member.getMemPw(), member.getMemMail(), member.getMemPhone1(), member.getMemPhone2(), member.getMemPhone3());

		// model.addAttribute("memId", memId);
		// model.addAttribute("memPw", memPw);
		// model.addAttribute("memMail", memMail);
		// model.addAttribute("memPhone", memPhone1 + "-" + memPhone2 + "-" + memPhone3);

		return "memJoinOk";
	}
}

```
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Home</title>
</head>
<body>
	<h1>memJoinOk</h1>
		ID : ${member.memId}<br />
		PW : ${member.memPw}<br />
		MAIL : ${member.memMail}<br />
		PHONE : ${member.memPhone1} - ${member.memPhone2} - ${member.memPhone3} <br />
		<input type="submit" value="Join">
		<input type="reset" value="Cancel">
	</form>
	<a href="/lec17/resources/html/login.html">LOGIN</a> &nbsp;&nbsp; <a href="/lec17/resources/html/memjoin.html">JOIN</a>
</html>
```

--------
> 2019-01-28
### 12-2. 어노테이션을 이용한 스프링 설정 - 2
#### 12-2-1 Java 파일분리
- 기존에 xml 파일을 만들어서 사용했고, 그것을 분리할 수 있었다.
- 똑같은 방식으로, java 파일도 분리해서 사용할 수 있다. 
- Ex) dao / service 객체 / db관련 / util 등 기능별로 구분
- MemberConfig1에서 @Bean으로 생성한 객체가 MemberConfig2에서 필요 → @Autowired로 주입해준다.
```java
//MainClassUseContifration.java
AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(MemberConfig1.class, MemberConfig2.class, MemberConfig3.class);
```

#### 12-2-2 @Import 이노테이션
```java
@Configuration
@Import({MemberConfig2, MemberConfig3})
public class MemberConfig1{
	... 
```
- import 구문을 안쓰는 것은 아니나, 많이 써보진 않음

### 13. 웹프로그래밍 설계모델
#### 13-1 웹프로그래밍을 구축하기 위한 설계 모델
- Model1 방식 <br>
Client <-> WAS(JSP<->Service&DAO)) <-> DB
→ 개발 속도가 빠름 / 유지보수가 어렵다.
- Model2 방식 (MVC) <br>
Client <-> WAS(Controller(<->View(JSP))<->Service(모듈화)<->DAO(모듈화))<->model<->DB <br>

#### 13-2 스프링 MVC 프레임워크 설계 구조
Client → DispatcherServlet <-> HanlderMapping / HandlerAdapter<->Controller <br>
	   → View → Client(응답 JSP) <br>
	   → ViewResolver <br>

HandlerMapping : 가장 적합한 Controller를 찾는다. <br>
HandlerAdapter : Controller 내에 적합한 Method를 찾는다. <br>
ViewResolver : 가장 적합한 JSP 페이지(View)를 찾는다. <br>

#### 13-3 DispatcherServlet 설정
- 사거리의 신호등과 같다.
- web.xml이 생소하면 JSP/Servlet 자료를 검색해서 선행학습하고 오세요.
```java
<servlet>
 <servlet-name>appServlet</servlet-name>
 <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
 <init-param>
  <param-name>contextConfigLocation</param-name>
  <param-value>/WEB-INF/spring/appServlet/servlet-context.xml</param-value> //스프링 설정파일
 </init-param>
 <load-on-startup>1</load-on-startup>
</servlet>
```
- 내가 실제로 작업할 것은 controller이랑 view 밖에 없다. 

#### 13-4 Controller 객체 - @Controller
DispatcherServlet <-> HandlerAdapter <-> Controller <br>
- Controller 객체로 사용할 클래서 정의 → 스프링 설정파일에 <code>annotation-driven</code> 후 <code>@Controller</code> <br>
```java
//servlet-context.xml

<annotation-driven />
```

```java
@Controller
public class HomeController{
	...
}
```

#### 13-5 Controller 객체 - @RequestMapping
DispatcherServlet <-> HandlerAdapter <-> Controller <br>
- Controller 안에 있는 Method는 <code>@RequestMapping</code> 어노테이션을 통해 매핑시켜준다. <br>
```java
@RequestMapping("/success")
public String success(Model model){

	return "success";
}
```

#### 13-6 Controller 객체 - Model 타입의 파라미터
DispatcherServlet <-> HandlerAdapter <-> Controller <-> Service / DAO / Etc. <br>
```java
@RequestMapping("/success")
public String success(Model model){
```
```java
model.setAttribute("tempData", "model has data!!");
```
→ 개발자는 Model 객체에 데이터를 담아서 DispatcherServlet에 전달할 수 있다. <br>
→ DispatcherServlet에 전달된 Model 데이터는 View에 가공되어 클라이언트한테 응답처리 된다.

#### 13-7 View 객체
DispatcherServlet <-> ViewResolver <-> View <br>
```java
<beans:bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"> //View를 찾는 viewResolver
 <beans:property name="prefix" value="/WEB-INF/views/" />
 <beans:property name="suffix" value=".jsp" />
</beans:bean>
```
→ JSP 파일명 : /WEB-INF/views/success.jsp

#### 13-8 전체적인 웹프로그래밍 구조
최초 사용자(Client) 요청(Ex: http://localhost:8090/ch08/success) <br> → DispatcherServlet(받음) / 스프링 프레임워크에 있는 것으로, web.xml에서 servlet 등록을 하고, 초기 파라미터로 스프링 설정파일을 설정한다. / Controller를 찾는다.(HandlerMapping이 찾는다. @Controller 어노테이션으로 Controller를 만듦) 적합한 Controller를 찾음 <br> → 다시 DispaterServlet으로 감. → 적합한 Method를 찾기 시작. <br> → 사용자 요청에 해당하는 메서드 실행(Ex: @RequestMapping("success") 어노테이션이 적용된 메서드 검색 및 실행 - Service -> DAO -> DB) → Model과 View의 형태로 Dispatcher Servlet으로 감. <br> → View 검색(Ex : ViewResolver에 의해서 검색된 Success.jsp 검색 및 실행 ) → View (Ex : 브라우저에 JSP를 이용한 응답) 

### 14. 스프링 MVVC 웹서비스 - 1
#### 14-1 웹 서버(Tomcat) 다운로드
- [Tomcat](https://tomcat.apache.org)

#### 14-2 웹 서버(Tomcat)와 이클립스 연동
- servers Tab → Apache - Tomcat v8.0 Server
- 더블클릭 → Server Locations - Use Tomcat installation
- Server Options - Publish module contexts to separate XML files Check
- Ports - HTTP/1.1 - 8090으로 수정 / 나중에 DB로 Oracle을 쓸건데 Oracle 내부 프로토콜이 8080이라서 충돌 방지
- Server Synchronized
- Start the Server
- localhost:8090 == 127.0.0.1:8090

#### 14-3 이클립스에 STS(Spring Tool Suit) 설치
- Eclipse Maketplace → Spring Tool Suit

#### 14-4 STS를 이용한 웹프로젝트 생성
- New Spring Legacy Project → Spring MVC Project → Project Setting "com.pjt.pjt14"

#### 14-5 스프링 MVC프레임워크를 이용한 웹프로젝트 분석
- src/java/com/pjt/pjt14/HomeController.java

### 15. 스프링 MVC 웹서비스 - 2
#### 15-1 프로젝트 전체 구조
- java파일 : java파일들이 위치한다. 주로 패키지로 묶어서 관리한다. 웹 어플리케이션에서 사용되는 Controller, Service, DAO 객체들이 위치한다.
- webbapp : 웹과 관련된 파일을(스프링 설정파일, JSP파일, HTML파일 등)이 위치한다.
- resources : JSP파일을 제외한 html, css, js파일 등이 위치한다.
- spring 폴더 : 스프링 컨테이너를 생성하기 위한 스프링 설정파일이 위치한다.(servlet-context.xml 등)
- views 폴더 : View로 사용될 JSP 파일이 위치한다.
- pom.xml 파일 : 메인 레파지토리에서 프로젝트에 필요한 라이브러리를 내려받기 위한 메이븐 설정 파일

#### 15-2 web.xml
- 웹 어플리케이션에서 최초 사용자의 요청이 발생하면 가장 먼저 DispatcherServlet이 사용자의 요청을 받는다고 하였다. 따라서 개발자는 DispatcherServlet을 서블릿으로 등록해주는 과정을 설정해주어야 한다. 그리고 사용자의 모든 요청을 받기 위해서 서블릿 맵핑 경로는 '/'로 설정한다.
- (1) HandlerMapping → DispatcherServlet → (2)HandlerAdapter → Controller → HandlerAdapter → DispatcherServlet → (3) ViewResolver → View
- 마지막으로 정리하자면, 요청이 들어오면 web.xml은 DispatcherServlet을 Servlet으로 등록시키고, Servlet으로 등록된 DispatcherServlet은 HandlerMaping(적절한 Controller 찾음), HandlerAdapter(적당한 method 찾음), ViewResolver(적당한 View 찾음)을 통해 웹서비스를 구현한다.

#### 15-3 DispatcherServlet
- 사용자의 모든 요청을 <code>DispatcherServlet</code>이 받은 후 <code>HandlerMapping</code> 객체에 Controller 객체 검색을 요청한다. 그러면 <code>HandlerMapping</code> 객체는 프로젝트에 존재하는 모든 <b>Controller</b> 객체를 검색한다. <code>HandlerMapping</code> 객체가 <b>Controller</b> 객체를 검색해서 <code>DispatcherServlet</code> 객체에 알려주면 <code>DispatcherServlet</code> 객체는 다시 <code>HandlerAdapter</code> 객체에 사용자의 요청에 부합하는 메소드 검색을 요청한다. 그러면 <code>HandlerAdapter</code> 객체는 사용자의 요청에 부합하는 메소드를 찾아서 해당 <b>Controller</b> 객체의 메소드를 실행한다. <b>Controller</b> 객체의 메소드가 실행된 후 <b>Controller</b> 객체는 <code>HandlerAdapter</code> 객체에 <b>ModelAndView</b> 객체를 반환하는데 <b>ModelAndView</b> 객체에는 사용자 응답에 필요한 데이터정보와 뷰정보(JSP파일)가 담겨있다. 다음으로 <code>HandlerAdapter</code> 객체는 <b>ModelAndView</b> 객체를 다시 <code>DispatcherServlet</code> 객체에 반환한다. <br>
→ HandlerMapping : 사용자의 요청에 부합하는 컨트롤러 검색 <br>
→ HandlerAdapter : 사용자의 요처에 부합하는 컨트롤러의 메서드 실행 요청 <br>
→ Controller : Bussiness 로직 수행 <br>

#### 15-4 servlet-context.xml
→ Servlet으로 등록될 때 contextConfigLocation 이름으로 초기화 파라미터를 servlet-context.xml로 지정하고 있는데 이 때 지정된 servlet-context.xml파일이 스프링 설정의 역할을 하는 파일이다. <br>
```java
//servlet-context.xml
<resources mapping="/resources/**" location="/resources/" />

<beans:property name="prefix" value="/WEB-INF/views/" />
<beans:property name="suffix" value=".jsp" />
```

#### 15-5 Controller(컨트롤러)
- Controller → Service → DAO <br>
- 사용자의 요청을 실제로 처리하는 객체들(실제로 개발자의 공수가 많이 투입된다.)
```java
@Controller
public class HomeController{

	@RequestMapping(value="/", method = RequestMethod.GET)
	public String home(Locale locale, Model model){
		Date date = new Date();
		DateFormat dateFormat = DateFormat.getDateTimeInstance(DateFormat.LONG, DateFormat.LONG, locale);

		String formattedDate = dateFormat.format(date);

		model.addAttribute("serverTime", formattedDate);

		return "home";
	}
}
```
→
```java
@RequestMapping("/success") //사용자로부터 '/success'요청이 발생하면 success() 메서드를 실행 // 사용자 요청에 대한 URL
public String success(Model model){ // success() 메서드 실행 후 뷰에서 활용되는 데이터를 담고 있는 객체

	return "success"; // 뷰로 사용되는 JSP 파일 이름
}
```

#### 15-6 View(뷰)
→ 메서드 반환값
```java
return "hoem";
```
→ JSP 파일
```java
/WEB-INF/views/home.jsp
```
→ 사용자 응답 브라우저 <br>
<code>http://localhost:8090/lec14/</code> <br>
 
--------
> 2019-01-25
### 12-1. 어노테이션을 이용한 스프링 설정-1
#### 12-1-1 : xml파일을 Java파일로 변경하기 <br>
- xml 코드를 java파일에서 어떻게 표현할 수 있을까 <br>
→ java 파일이 xml을 대신해서 스프링 컨테이너를 생성할 수 있어야 한다. <br>
→ MemberConfig(.java)파일이 스프링 컨테이너를 생성할 수 있습니다 라고 명시해줘야 함 → 이 때 사용하는 어노테이션이 <code>@Configuration</code> <br>
→ 또한 java 파일에서는 빈(Bean) 태그의 class명, id값 순으로 적어준다. <br>
→ 또한, <code>@Bean</code> 어노테이션을 달아준다. <br>
```java
@Configuration
public class MemberConfig{
	//<bean id="studentDao" class="ems.member.dao.StudentDao"></bean>
	@Bean
	public StudentDao studentDao(){ //Bean Tag Class, id
		return new StudentDao();
	}
}
```
→ constructor-arg로 받을 경우 <br> 
```java
	/*
	<bean id="registerService" class="ems.member.service.StudentRegisterService">
	  <constructor-arg ref="studentDao"></constructor-arg>
	</bean> */
	@Bean
	public StudentRegisterService registerService(){ //Bean Tag Class, id
		return new StudentRegisterService(studentDao); //ref
	}
```
→ property의 경우 <br>
```java
// .xml
<bean id="dataBaseConnectionInfoDev" class="ems.member.dataBaseConnectionInfo">
 <property name="jdbcUrl" value="jdbc:oracle:thin:@localhost:1521:xe" />
 <property name="userId" value="scott" />
 <property name="userPd" value="tiger" />
</bean>
```
→
```java
//.java
@Bean
public DataBaseConnectionInfo dataBaseConnectionInfoDev(){
	DaaBaseConnectionInfo inforDev = new DataBaseConnectionInfo();
	inforDev.setJdbcUrl("jdbc:oracle:thin:@localhost:1521:xe");
	inforDev.setUserId("scott");
	inforDev.setUserPw("tiger");

	return inforDev;
}
```
→ value, list, map을 넣어줄 경우 <br>
```java
/*
//.xml
<bean id="informationService" class="ems.member.service.EMSInformationService">
 <property name="ver">
   <value>The version is 1.0</value>
 </property>
 <property name="sYear">
   <value>2015</value>
 </property>
 <property name="sMonth">
   <value>1</value>
 </property>
 <property name="developers" />
   <list>
     <value>Cheney.</value>
     <value>Eloy.</value>
     <value>Jasper.</value>
   </list>
 </property>
 <property name="administrators">
   <map>
     <entry>
       <key>
         <value>Cheney</value>
       </key>
       <value>cheney@springPjt.org</value>
     </entry>
     <entry>
       <key>
         <value>Jasper</value>
       </key>
       <value>jasper@springPjt.org</value>
     </entry>
   </map>
 </property>
 <property name="dbInfos">
   <map>
     <entry>
        <key>
          <value>dev</value>
        </key>
        <ref bean="dataBaseConnectionInfoDev" />
     <entry>
   </map>
 </property>
</bean>
*/

//.java
@Bean
public EMSInformationService informationService(){
	EMSInformationService info = new EMSInformationService();

	//EMSInformationService.java 참고
	info.setVer("The version is 1.0");
	info.setsYear(2015);
	info.setsMonth(1); 

	ArrayList<String> developers = new ArrayList<String>();
	developers.add("Cheney.");
	developers.add("Eloy.");
	developers.add("Jasper.");
	info.setDevelopers(developers);
    
    Map<String, String> administrators = new HashMap<String, String>();
    administrators.put("Cheny", "cheney@springPjt.org");
    administrators.put("Jasper", "jasper@springPjt.org");
    info.setAdministrators(administrators);

    Map<String, DataBaseConnectionInfo> dbInfos = new HashMap<String, DataBaseConnectionInfo>();
    dbInfos.put("dev", dataBaseConnectionInfoDev());
    info.setDbinfos(dbInfos);

	return info;
}
```
→ 기존에 MainClassUseXml.java에서 아래의 코드를 사용하였다.<br>
```java
// MainClassUseXml.java
GenericXmlApplicationContext ctx = new GenericXmlApplicationContext("classpath:applicationContext.xml");
```
→ 그런데 .java 파일 즉, MemberConfig.java 파일에서 .xml 대신 빈(Bean) 객체를 생성해주고 있으므로, MainClassUseXml.java에서 다른 선언이 필요하다. <br>
```java
// MainClassUseXml.java
AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(MemberConfig.class);
```


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