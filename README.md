TIL(Today I Learned)
====================

Spring
-------
> 2019-01-21
> 자료 : 자바 스프링 프레임워크(ver.2018) – 신입 프로그래머를 위한 [강좌](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC_renew/)
#### 1. 스프링 개요
#### 2. 개발 환경 구축
#### 3. 스프링 프로젝트 생성 : Maven을 이용해서 스프링 프로젝트를 생성하는 방법에 대하여 학습
- 프로젝트 생성
- pom.xml 작성
- 폴더 및 pom.xml 파일의 이해
: pom.xml 파일은 메이븐 설정 파일로 메이븐은 라이브러리를 연결해주고, 빌드를 위한 플랫폼이다. → 외부 레파지토리에서 내꺼로 다운로드 해준다
#### 4. 처음해 보는 스프링 프로젝트
- dependency 태그→ 내가 필요한 모듈
- bulid 태그 → 빌드할 때 필요한 명령들
- Spring만이 가지고 있는 기능들
- 스프링컨테이너(ApplicationContext)의 객체 -> bean(Object)
- 객체 생성 -> 메모리에 로드되었다는 것 / ApplicationCOntext에 있다는 것은 New 키워드가 필요없음 -> 객체 생성되어있음
#### 5. 또 다른 프로젝트 생성방법
- 일일히 다 만드는 방법
- bean의 id는 고유한 id, class는 패키지 포함한 내용

Next 6. DI(Dependency Injection)