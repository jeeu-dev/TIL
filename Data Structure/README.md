C/C++/자료구조
====================

> 자료 : [패스트캠퍼스 컴퓨터 공학 올인원 패키지](https://www.fastcampus.co.kr/dev_online_cs/)
> 
> 수강 사이트 : https://online.fastcampus.co.kr
-------
> 2019-02-28

#### 0강 - 인트로

1. C언어 기초 문법
2. 자료구조 시초 및 심화이론 

#### 1강 - 프로그래밍 개발환경 구축하기
소스 코드부터 실행파일까지
: 설계도 →(에디터)→ 소스코드 →(전처리기)→ 향상된 소스코드 → (컴파일러) → 목적코드 → (링커) → 실행파일 

#### 2강 - 변수와 상수
라이브러리 불러오기

변수의 초기화와 쓰레기 값

1) 정적 변수로 선언된 것은 기본적으로 0으로 초기화

2) 정적 변수가 아닌 수를 0으로 초기화 하려면 값을 일일이 넣어주어야 한다.

변수와 상수

예약어와 식별자

정수의 표현방법
:  부호 절대값 방식 → 부호 비트 - 맨 앞 양수:0 / 음수:1
:  실제로는 2의 보수 방식 사용 - 2의 보수 = 1의 보수(모든 비트 뒤집기) + 1 / 이 때 올림 수가 발생하면 무시

실수의 표현방법
1) 지수부, 유효숫자부 나누어서 표현. 

#### 3강 기본 입출력

`scanf("%d", &a);` → 실제로는 잘 사용하지 않음 / 취약한 함수임

실수형을 입력받아서 소수점 셋째 자리까지 출력하기

```C
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int main(void){
    double a;
    scanf("%lf", &a);
    printf("%.2f\n", a);
    system("pause");
    return 0;
}
```

#### 4강 연산자

`%`  : 모듈러(Modular)연산 - 나머지 구하기, `\"` : 큰따옴표, `\t` : Tab

논리 연산자 `!`: 부정, `&&` : 그리고, `||`: 또는

비트 연산자 `~`: 부정, `&`: 그리고, `|`: 또는, `^`: 배타적, `<<`: 왼쪽 시프트

* 시프트 연산자가 많이 쓰임.

#### 5강 조건문

#### 6강 반복문

#### 7강 함수

재귀함수 - 자기자신을 포함하는 함수, 기본적으로 자기자신을 계속 불러낸다. 반드시 재귀종료 조건이 필요하다.
Ex) 재귀함수를 이용한 팩토리얼

#### 8강 배열

- 배열을 사용하면 동일한 성격의 데이터를 다수 표현할 수 있다.
- 배열의 선언과 초기화 : 자료형 배열명[배열의 크기] = {초기화 값}; *초기화 값은 없을 수도 있음
- `INT_MIN` : 최댓값을 구하기 위해 자주 사용되는 기능, `<limits.h>` 헤더 파일에 정의가 되어있는 것으로 int형 범위의 최솟값을 반환. `INT_MAX` 또한 사용 가능
- c언어는 기본적으로 자체적인 문자열 자료형 제공하지 않음. c언어에서는 문자를 여러 개 묶어 놓는 형태로 문자열 표현, c++에서는 이러한 불편함을 알고 있기 때문에 자체적으로 String 자료형 제공.

#### 9강 포인터

- 메모리 주소를 저장한다.
  → 포인터는 특정한 변수 자체가 존재하는 메모리 주소의 값을 가진다.

  ```c
  int a = 5; // a의 값 : 5 | 주소 : 0xAFB03954
  
  int *b = &a; // b의 값 : 0xAFB03954 | 주소 : 0xCA29839F
  ```

  - 주소 연산자(&) : 변수 앞에 붙어서 변수의 메모리 시작 주소 값을 반환
  - 포인터(*) : 포인터변수를 선언할 때 사용
  - 간접참조 연산자(*) : 선언된 포인터 변수가 가리키는 변수를 구한다

- 포인터는 컴퓨터 시스템의 특정한 메모리에 바로 접근할 수 있습니다.

- **따라서 기존에 존재하던 중요한 메모리 영역에 접근하지 않도록 해야 합니다.**

- 다음과 같은 코드는 굉장히 위험한 코드입니다.

  ```c
  int *a =0x33484735;
  *a = 0;
  ```

> 2019-03-07

### 10강 - 문자

- C 언어의 문자는 아스키 코드를 따른다.
- 아스키 코드는 0~127 중의 1바이트로 구성되며 주요 문자를 출력하도록 해준다.
- 문자열을 처리할 때 버퍼의 개념이 많이 사용됩니다.
  - 버퍼(Buffer)란 임시적으로 특정한 데이터를 저장하기 위한 목적으로 사용됩니다.
  - C언어는 기본적으로 사용자가 의도하지 않아도 자동으로 버퍼를 이용해 입출력을 처리합니다.

### 11강 - 문자열

- 문자열은 컴퓨터 메모리 구조상에서 마지막에 널(NULL) 값을 포함한다.
- 널(NULL) 값은 문자열의 끝을 알리는 목적으로 사용
- 문자열과 포인터
  - **문자열** 형태로 **포인터**를 사용하면 포인터에 **특정한 문자열의 주소**를 넣게 됩니다.
  - "Hello World" 문자열을 읽기 전용으로 메모리 공간에 넣은 뒤에 그 위치를 처리한다.
  - 이러한 문자열을 '문자열 리터럴'이라고 말한다. 이는 컴파일러가 알아서 메모리 주소를 결정한다.
  - 포인터로 문자열을 선언했다고 하더라도 기존의 배열처럼 처리할 수 있다.
- 문자열 입출력 함수
  - scanf() 함수는 공백을 만날 때까지 입력받지만 **gets() 함수**는 **공백까지 포함하여 한줄**을 입력받는다.
  - gets() 함수는 버퍼의 크기를 벗어나도 입력을 받아버린다.
  - C11 표준부터는 버퍼의 크기를 철저히 지키는 gets_s() 함수가 추가되었다.
  - gets_s()를 이용하는 경우 범위를 넘으면 그 즉시 런타임(Runtime) 오류가 발생하게 된다.
- C언어의 문자열처리 관련해서는 기본적인 문자열 함수를 알고 있는 것이 좋다.
- 나중에 C++을 이용하면 더욱 간편하고 다양한 함수를 사용할 수 있다.
- C언어에서의 문자열 함수는 <string.h> 라이브러리에 포함되어 있다.
- strlen()는 문자열의 길이를 반환한다.
- strcmp()는 문자열 1이 문자열 2보다 사전적으로 앞에 있으면 -1, 뒤에 있으면 1을 반환한다.
- strcpy()는 문자열을 복사한다.
- **C언어에서는 기본적으로 'a=b'와 같은 간단한 방식으로는 문자열 복사 안된다.**
- strcat()은 뒤에 있는 문자열을 앞에 있는 문자열에 합친다.
- strstr()은 긴 문자열에서 짧은 문자열을 찾아 그 위치를 반환한다.
- 짧은 문자열을 찾은 주소 값 자체를 반환하므로 단순히 출력하도록 하면, 찾은 이후 모든 문자열이 반환된다.

> 2019-03-08

### 12강 - 컴퓨터가 변수를 처리하는 방법

프로그램 메모리 주소

- 컴퓨터에서 프로그램이 실행되기 위해서는 프로그램이 메모리에 적재(Load) 되야 한다.
- 당연히 프로그램의 크기를 충당할 수 있을 만큼의 공간이 있어야 한다.
- 일반적인 컴퓨터의 운영체제는 메모리 공간을 네가지로 구분하여 관리한다.
  **코드 영역**(소스코드), **데이터 영역**(전역변수/정적변수), **힙 영역**(동적 할당 변수), **스택 영역**(지역 변수/매개변수)

**전역변수**란 프로그램의 어디서든 접근 가능한 변수

- main 함수가 실행되기도 전에 프로그램의 시작과 동시에 메모리에 할당
- 프로그램의 크기가 커질 수록 전역 변수로 인해 프로그램이 복잡해질 수 있음
- 메모리의 **데이터(Data) 영역**에 적재

**지역변수**란 프로그램에서 특정한 블록에서만 접근할 수 있는 변수

- 함수가 실행될 때마다 메모리에 할당되어 함수가 종료되면 메모리에서 해제된다.
- 메모리의 **스택(Stack) 영역**에 기록

**정적변수(Static Variable)**란 특정한 블록에서만 접근할 수 있는 변수  / 지역변수와 전역변수의 특징 모두 가짐

- 프로그램이 실행될 때 메모리에 할당되어 프로그램이 종료되면 메모리에서 해제된다.
- 메모리 **데이터(Data) 영역**에 적재

**레지스터 변수** 

- 레지스터 변수(Register Variable)란 메인 메모리 대신 CPU의 레지스터를 사용하는 변수
- 레지스터는 매우 한정되어 있으므로 실제로 레지스터에서 처리될지는 장담할 수 없다. 
- 더 빠르게 처리되리라 기대할 수 있다.

함수의 매개변수가 처리될 때

- 함수를 호출할 때 함수에 필요한 데이터를 매개변수로 전달한다.
- 전달 방식은 <값에 의한 전달> 방식과 <참조에 의한 전달> 방식이 있다.
- **값에 의한 전달 방식**은 단지 **값을 전달**하므로 함수 내에서 **변수가 새롭게 생성**된다.
- **참조에 의한 전달 방식**은 **주소를 전달**하므로 **원래의 변수 자체에 접근**할 수 있다. 
  - 참조에 의한 전달 방식은 단지 매개변수로 '포인터(Pointer)' 변수를 보낼 뿐 딱히 특별한 게 아니다. 

### 13강 - 다차원 배열과 포인터 배열

2차원 배열의 초기화

- 2차원 배열은 1차원 배열이 중첩되었다는 의미로 [] (대괄호) 두번 연속해서 쓴다
  기본적으로 행이 먼저 들어간다.

  ```c
  int a[3][3] = { {1,2,3}, {4,5,6},{7,8,9}};
  ```

포인터 배열의 구조 분석

- 배열은 포인터와 동일한 방식으로 동작
- 배열의 이름은 배열의 원소의 첫번째 주소가 된다
- 유일한 차이점이라고 하면, 포인터는 변수이며 배열의 이름 상수이다.
- 포인터는 연산을 통해 자료형의 크기만큼 이동한다.
  - 따라서 정수(int)형 포인터는 4바이트(Bytes)씩 이동한다.

### 14강 - 동적 메모리 할당

- 일반적으로 C언어에서 배열의 경우 사전에 적절한 크기만큼 할당해주어야 한다.
- 우리가 원하는 만큼만 메모리를 할당해서 사용하고자 한다면 동적 메모리 할당을 사용한다.
- 동적이라는 말의 의미는 '프로그램 실행 도중에'라는 의미

동적 메모리 할당 함수

- C언어에서는 malloc() 함수를 이용해 원하는 만큼의 메모리 공간을 확보 할 수 있다.

- malloc() 함수는 메모리 할당에 성공하면 주소를 반환하고, 그렇지 않으면 NULL을 반환한다.

- malloc() 함수는 <stdlib.h> 라이브러리에 정의되어 있다.

  ```c
  malloc(할당할 바이트 크기);
  ```

- 동적으로 할당된 변수는 <힙 영역>에 저장된다.

- 전통적인 C언어에서는 스택에 선언된 변수는 따로 메모리 해제를 해주지 않아도 된다.

- 반면에 **동적으로 할당된 변수는 반드시 free() 함수**로 **메모리 해제**를 해주어야 한다.

- 메모리 해제를 하지 않으면 메모리 내의 프로세스 무게가 더해져 언젠가는 오류가 발생한다.

- 메모리 누수(Memory Leak) 방지는 코어 개발자의 핵심 역량이다.

동적으로 문자열 처리하기

- 일괄적인 범위의 메모리를 모두 특정한 값으로 설정하기 위해서는 memset()을 사용한다.
- memset(포인터, 값, 크기);
- 한 바이트 씩 값을 저장하므로 문자열 배열의 처리 방식과 흡사하다.
- 따라서 memset() 함수는 <string.h> 라이브러리에 선언되어 있다.

> 2019-03-11

### 15강 - 함수 포인터

- C언어에서는 함수의 이름을 이용해 특정한 함수를 호출한다.
- 함수 이름은 메모리 주소를 반환한다.

- 함수 포인터는 특정한 함수의 반환 자료형을 지정하는 방식으로 선언할 수 있다.

- 함수 포인터를 이용하면 형태가 같은 서로 다른 기능의 함수를 선택적으로 사용할 수 있습니다.

- ```
  반환 자료형(*이름)(매개별수) = 함수명;
  ```

- ```c
  #include <stdio.h>
  
  void myFunction(){
      printf("It's my function");
  }
  
  void yourFunction(){
      printf("It's your function");
  }
  
  int main(void){
      void(*fp)() = myFunction;
      fp();
      fp = yourFunction;
      fp();
      system("pause");
      return 0;
  }
  ```

- 함수 포인터를 반환하여 사용하기

  ```c
  #include <stdio.h>
  
  int add(int a, int b){
      return a + b;
  }
  
  int(*process(char* a))(int, int){
      printf("%s\n", a);
      return add;
  }
  
  int main(void){
      int(*fp)(int, int) = add;
      printf("%d\n", fp(10, 30));
      fp = sub;
      printf("%d\n", process("10 + 20 = ?")(10, 20));
      system("pause");
      return 0;
  }
  ```

  - 잘 안쓴다. 필요할 때 구글링. 

### 16강 - 구조체

- 여러개의 변수를 묶어 **하나의 객체**를 표현하고자 할 때 구조체를 사용할 수 있다.

- 캐릭터, 몬스터, 학생, 좌표 등 다양한 객체를 모두 프로그래밍 언어를 이용해 표현할 수 있다.

- ```c
  struct 구조체명{
      자료형1 변수명1;
      자료형2 변수명2;
  }
  ```

- ```c
  struct Student{
      char studentId[10];
      char name[10];
      int grade;
      int major;
  }
  ```

- 구조체의 변수의 선언과 접근

  - 기본적으로 구조체의 변수에 접근할 때는 온점(.)을 사용한다.

    ```c
    struct Student s; //구조체 변수 선언
    strcpy(s.studentId, "00000000"); //구조체 변수에 접근
    strcpy(s.name, "ooo");
    s.grade = 4;
    strcpy(s.major, "OOO OOO");
    ```

- 구조체의 정의와 선언

  - 하나의 구조체 변수만 사용하는 경우 정의와 동시에 선언을 할 수도 있다.

  - 이 경우 변수는 전역 변수로 사용된다.

    ```c
    struct Student{ // 학생 구조체 정의 및 선언
      char studentId[10];
      char name[10];
      int grade;
      char major[51];  
    } s;
    ```

- 구조체의 초기화

  - 구조체의 변수를 한 번에 초기화하기 위해서는 중괄호에 차례대로 변수의 값을 넣는다.

    ```c
    struct Student s = {"000000", "OOO", 1, "OOOOOO"};
    ```

- 더 짧게 구조체 정의하기

  - typedef 키워드를 이용하면 임의의 자료형을 만들 수 있으므로 선언이 더 짧아진다.

    ```c
    typedef struct Student{
        char studentId[10];
        ...
    } Student;
    ```

  - 최근에는 익명 구조체의 개념이 등장하여, 구조체 이름 부분을 비워놔도 된다.

    ```c
    typedef struct{ //학생 구조체 정의
        ...
    } Student
    ```

- 구조체 포인터 변수에 접근하기

  - 구조체가 포인터 변수로 사용되는 경우 변수에 접근할 때 화살표 (->)를 사용합니다.

    ```c
    int main(void){
        Student *s = malloc(sizeof(Student));
        
        printf("학번: %s\n", s->studentId);
        printf("이름: %s\n", s->name);
        system("pause");
        return 0;
    }
    ```

### 17강 - 파일 입출력

- 프로그램이 꺼진 이후에도 데이터를 저장하기 위해서는 파일 입출력이 필요
- 파일을 열고 닫기
  - 파일 입출력 변수는 FILE 형식의 포인터 변수로 선언합니다.
  - 파일을 열 떄는 fopen() 함수를 이용합니다.
    - 파일경로와 접근 방식을 설정할 수 있습니다. 
    - r : 읽기, w : 쓰기, a : 접근하여 데이터를 뒤에서부터 기록
  - 파일을 닫을 때는 fclose() 함수를 이용합니다.

- 파일 입출력 함수

  - 기본적인 입출력을 위해서 printf()와 scanf() 함수를 사용하곤 했습니다.
  - 파일 입출력에서는 그 대신에 fprintf()와 fscanf()가 사용된다.
    fprintf(파일 포인터, 서식, 형식지정자);
    fscanf(파일 포인터, 서식, 형식지정자);

- 파일 입출력의 과정

  - 파일 입출력은 열고, 읽고/쓰고, 닫기의 과정을 철저히 따라야 한다.
  - 파일을 열 때는 파일 포인터가 사용되며, 이는 동적으로 할당된 것
  - 따라서 파일 처리 이후에 파일을 닫아주지 않으면 메모리 누수가 발생

- ```c
  #define _CRT_SECURE_NO_WARNINGS
  #include <stdio.h>
  
  int main(void){
      char s[20] = "Hello World";
      FILE *fp;
      fp = fopen("temp.txt", "w");
      fprintf(fp, "%s\n", s);
      fclose(fp);
      return 0;
  }
  ```

### 18강 - 전처리기

- 전처리기 구문은 다른 프로그램 영역과 독립적으로 처리된다.
- 전처리기 구문은 소스코드 파일 단위로 효력이 존재한다.

- 파일 포함 전처리기
  - #include는 전처리기에서 가장 많이 사용되는 문법
  - 특정한 파일을 라이브러리로서 포함시키기 위해 사용
  - #include 구문으로 가져 올 수 있는 파일에는 제약이 없다.
- #include <파일 이름>
  - 이와 같이 선언하면 시스템 디렉토리에서 파일을 검색한다.
  - 운영체제마다 시스템 디렉토리가 존재하는 경로가 다를 수 있다.
  - 대표적으로 stdio.h와 같은 헤더 파일 등이 시스템 디렉토리에 존재한다.
- #include "파일 이름"
  - 이와 같이 선언하면 현재 폴더에서 파일을 먼저 검색한다.
  - 만약 현재 폴더에 파일이 없다면 시스템 디렉토리에서 파일을 검색한다. 

- 매크로 전처리기

  - 프로그램 내에서 사용되는 상수나 함수를 매크로 형태로 저장하기 위해 사용
  - #define 문법을 사용해 정의할 수 있다.
  - 인자를 가지는 매크로 전처리기
    - #define 문법에는 인자가 포함될 수 있다.
    - #define 문법은 소스코드의 양을 획기적으로 줄이는 데 도움을 준다.

- 조건부 컴파일

  - 컴파일이 이루어지는 영역을 지정하는 기법
  - 일반적으로 디버깅과 소스코드 이식을 목적으로 하여 작성
  - C언어로 시스템 프로그램을 작성할 때에는 운영체제에 따라서 소스코드가 달라질 수 있음
  - 이 때 운영체제에 따라서 컴파일이 수행되는 소스코드를 다르게 할 수 있다.
  - #ifndef ~ #endif 문법은 대표적인 조건부 컴파일 문법
  - 흔히 헤더 파일의 내용이 중복되어 사용되지 않도록 하기 위해 적는다.

- 파일 분할 컴파일

  - 일반적으로 자신이 직접 라이브러리를 만들 때에는 C언어 파일과, 헤더 파일을 모두 작성해야 한다.

    ```c
    // main.c
    #include <stdio.h>
    #include "temp.h"
    
    int main(void){
        printf("%d\n", add(3,5));
        system("pause");
        return 0;
    }
    
    // temp.h
    #ifndef _TEMP_H_
    #define _TEMP_H_
    int add(int a, int b);
    #endif
    
    //temp.c
    #include "temp.h"
    
    int add(int a, int b){
        return a + b;
    }
    ```

> 2019-03-13

### 19강 - 자료구조의 개요

- 기본적인 자료구조들
  - 선형구조 - 배열 / 연결 리스트 / 스택 / 큐
  - 비선형 구조 - 트리 / 그래프
- 프로그램의 성능 측정 방법론
  - 시간 복잡도(Time Complexity)란 알고리즘에 사용되는 연산 횟수를 의미
  - 공간 복잡도(Space Complexity)란 알고리즘에 사용되는 메모리의 양 의미
  - 효율적인 알고리즘을 사용한다고 했을 때 일반적으로 시간과 공간은 반비례 관계
- 프로그램의 성능 측정 방법론
  - 시간 복잡도를 표현할 때는 최악의 경우를 나타내는 Big-O 표기법을 사용
  - n이 1000일 때?
    - n : 1,000번의 연산
    - nlogn : 약 10,000번의 연산
    - n^2 : 1,000,000번의 연산
    - n^3 : 1,000,000,000번의 연산
  - **보통 연산 횟수가 10억을 넘어가면 1초 이상의 시간이 소요됩니다**
- 시간 복잡도를 표기할 때는 항상 큰 항과 계수만 표시합니다.
  Ex) O(3n^2 + n ) = O(n^2)
- 현실적인 다양한 문제에서는 시간 제한이 1초 정도라고 생각

- 공간 복잡도를 표기할 때는 일반적으로 MB 단위로 표기한다.
  int a[1000] : 4KB
  int a[1000000] : 4MB
  int a[2000] [2000] : 16MB

### 20강 - 연결 리스트

- 일반적으로 배열을 사용하여 데이터를 순차적으로 저장하고, 나열할 수 있다.

- 배열을 사용하는 경우 메모리 공간이 불필요하게 낭비 될 수 있다.

- 배열 기반의 리스트

  ```c
  #include <stdio.h>
  #define INF 10000
  
  int arr[INF];
  int count = 0;
  
  void addBack(int data){
      arr[count] = data;
      count ++;
  }
  
  void addFirst(int data){ // 뒤쪽부터 앞쪽까지 옮겨준다
      for(int i = count; i>=1; i--){
          arr[i] = arr[i-1];
      }
      arr[0] = data;
      count++;
  }
  ```

- 특정한 위치의 원소를 삭제하는 함수는 어떻게 만들 수 있을까?

  1. 특정한 위치의 원소를 삭제하는 removeAt() 함수는 다음과 같이 구현

     ```c
     void removeAt(int index){
         for(int i = index; i < count-1; i++){
             arr[i] = arr[i+1];
         }
         count--;
     }
     ```

- 배열 기반 리스트의 특징

  1. 배열로 만들었으므로 특정한 위치의 원소에 즉시 접근할 수 있다는 장점
  2. 데이터가 들어갈 공간을 미리 메모리에 할당해야 한다는 단점
  3. 원하는 위치로의 삽입이나 삭제가 비효율적

- 연결리스트

  1. 일반적으로 연결 리스트는 구조체와 포인터를 함께 사용하여 구현
  2. 연결 리스트는 리스트의 중간 지점에 노드를 구가하거나 삭제할 수 있어야 함
  3. 필요할 때마다 메모리 공간을 할당

  - 포인터를 이용해 **단방향적**으로 다음 노드를 가리킴
  - 일반적으로 연결 리스트의 시작 노드를 헤드(Head)라고 하여 별도로 관리
  - 다음 노드가 없는 끝 노드의 다음 위치 값으로 NULL을 넣음

- 연결 리스트 구조체 만들기

  ```c
  #include <stdio.h>
  #include <stdlib.h>
  
  typedef struct{
      int data;
      struct Node *next;
  } Node;
  
  Node *head;
  
  int main(void){
      head = (Node*)malloc(sizeof(Node));
      Node *node1 = (Node*)malloc(sizeof(Node));
      node1->data = 1;
      Node *node2 = (Node*)malloc(sizeof(Node));
      node1->data = 2;
      head->next = node1;
      node1->next = node2;
      node2->next = NULL;
      Node *cur = head->next;
      while (cur != NULL){
          printf("%d ", cur->data);
          cur = cur->next;
      }
      system("pause");
      return 0;
  }
  ```

- 연결 리스트 메모리 해제 함수

  ```c
  void freeAll(Node *root){
      Node *cur = head->next;
      While (cur != NULL){
          Node *next = cul->next;
          free(cur);
          cur = next;
      }
  }
  ```

- 연결 리스트 전체 출력 함수

  ```c
  void showAll(Node *root)){
      Node *cur = head->next;
      while(cur != NULL){
          printf("%d ", cur->data);
          cur = cur->next;
      }
  }
  ```

- 완성된 연결 리스트 사용하기

  ```c
  int main(void){
      head = (Node*) malloc(sizeof(Node));
      head->next = NULL;
      addFront(head, 2);
      addFront(head, 1);
      addFront(head, 7);
      addFront(head, 9);
      addFront(head, 8);
      removeFront(head);
      showAll(head);
      freeAll(head);
      system("pause");
      return 0;
  }
  ```

- 연결 리스트 구현에 있어서 주의할 점
  1. 위 소스코드에 덧붙여서 삽입 및 삭제 기능에서의 예외 사항을 처리할 필요가 있다.
  2. 삭제할 원소가 없는데 삭제하는 경우, 머리(Head) 노드 자체를 잘못 넣은 경우 등을 체크해야 한다.
- 연결 리스트의 특징
  1. 삽입과 삭제가 배열에 비해서 간단하다는 장점
  2. 배열과 다르게 특정 인덱스로 즉시 접근하지 못하며, 원소를 차례대로 검색해야함
  3. 추가적인 포인터 변수가 사용되므로 메모리 공간이 낭비

- 정리
  1. 연결 리스트는 데이터를 선형적으로 저장하고 처리하는 방법
  2. 기존에 배열을 이용했을 때보다 삽입과 삭제가 많은 경우에 효율적
  3. 다만 특정한 인덱스에 바로 참조해야 할 때가 많다면 배열을 이용하는 것이 효율적

### 21강 - 양방향 연결 리스트

- 양방향 연결 리스트

  - 양방향 연결 리스트는 머리(Head)와 꼬리(Tail)를 모두 가진다
  - 양방향 연결 리스트의 각 노드는 앞 노드와 뒤 노드의 정보를 모두 저장
  - 우리는 데이터를 '오름차순'으로 저장하는 양방향 연결 리스트를 구현

- 양방향 연결 리스트 선언하기

  ```c
  #include <stdio.h>
  #include <stdlib.h>
  
  typedef struct{
      int data;
      struct Node *prev;
      struct Node *next;
  } Node;
  
  Node *head, *tail;
  ```

- 양방향 연결 리스트 삽입 함수

  ```c
  void insert(int data){
      Node* node = (Node*) malloc(sizeof(Node));
      node->data = data;
      Node* cur;
      cur = head->next;
      while(cur->data) < data && cur != tail){
          cur = cur->next;
      }
      Node* prev = cur->prev;
      prev->next = node;
      node->prev = prev;
      cur->prev = node;
      node->next = cur;
  }
  ```

- 양방향 연결 리스트 삭제 함수

  ```c
  void removeFront(){
      Node* node = head->next;
      head->next = node->next;
      Node* next = node->next;
      next->prev = head;
      free(node);
  }
  ```

- 완성된 양방향 연결 리스트 사용하기

  ```c
  int main(void){
      head = (Node*) malloc(sizeof(Node));
      tail = (Node*) malloc(sizeof(Node));
      head->next = tail;
      head->prev = head;
      tail->next = tail;
      tail->prev = head;
      insert(2);
      insert(1);
      insert(3);
      insert(9);
      insert(7);
      removeFront();
      show();
      system("pause");
      return 0;
  }
  ```

- 양방향 연결 리스트 구현에 있어서 주의할 점

  1. 위 소스 코드에 덧붙여서 삽입 및 삭제 기능에서의 예외 사항을 처리할 필요가 있다.
  2. 더 이상 삭제할 원소가 없는데 삭제하는 경우 등을 체크해야 한다. 

- 정리
  - 양방향 연결 리스트
    1. 양방향 연결 리스트에서는 각 노드가 앞 노드와 뒤 노드의 정보를 저장하고 있다.
    2. 양방향 연결 리스트를 이용하면 리스트의 앞에서부터 혹은 뒤에서부터 모두 접근할 수 있다.

> 2019-03-14

### 22강 - 스택

- 스택(Stack)은 한쪽으로 들어가서 한쪽을 나오는 자료구조(Data Structure)이다.
- 이러한 특성 때문에 수식 계산 등의 알고리즘에서 다방면으로 활용
  - PUSH : 스택에 데이터를 넣는다.
  - POP : 스택에서 데이터를 빼낸다.

- 스택의 구현

  - 스택(Stack)은 배열을 이용한 구현 방법과 연결 리스트를 이용한 구현 방법으로 나누어진다.
  - 가장 기본적인 형태의 자료구조로 구현 난이도는 낮은 편이다.

- 배열을 이용한 스택 구현

  - 스택의 선언

    ```c
    #include <stdio.h>
    #define SIZE 10000
    #define INF 99999999
    
    int stack[SIZE];
    int top = -1;
    ```

  - 스택 삽입 함수

    ```c
    void push(int data){
        if (top == SIZE - 1){
            printf("스택 오버플로우가 발생했습니다.\n");
            return;
        }
        stack[++top] = data;
    }
    ```

  - 스택 추출 함수

    ```c
    int pop(){
        if(top == -1){
            printf("스택 언더플로우가 발생했습니다.\n");
            return -INF;
        }
        return stack[top--];
    }
    ```

  - 스택 전체 출력 함수

    ```c
    void show(){
        printf("--- 스택의 최상단 ---\n");
        for(int i = top; i>=0; i--){
            printf("%d\n", stack[i]);
        }
        printf("--- 스택의 최하단 ---\n");
    }
    ```

  - 완성된 스택 사용하기

    ```c
    int main(void){
        push(7);
        push(5);
        push(4);
        pop();
        push(6);
        pop();
        show();
        system("pause");
        return 0;
    }
    ```

- 연결 리스트를 이용한 스택 구현

  - 스택의 선언

    ```c
    #include <stdio.h>
    #include <stdlib.h>
    #define INF 99999999
    
    typedef struct{
        int data;
        struct Node *next;
    } Node;
    
    typedef struct{
        Node *top;
    } Stack;
    ```

- 배열을 이용한 스택 구현

  - 스택 삽입 함수

    ```c
    void push(Stack *stack, int data){
        Node *node = (Node*) malloc(sizeof(Node));
        node->data = data;
        node->next = stack->top;
        stack->top = node;
    }
    ```

  - 스택 추출 함수

    ```c
    int pop(Stack *stack){
        if(stack->top == NULL){
            printf("스택 언더플로우가 발생했습니다.\n");
            return -INF;
        }
        NOde *node = stack->top;
        int data = node->data;
        stack->top = node->next;
        free(node);
        return data;
    }
    ```

  - 스택 전체 출력 함수

    ```c
    void show(Stack *stack){
        Node *cur = stack->top;
        printf("--- 스택의 최상단 ---\n");
        while(cur != NULL){
            printf("%d\n", cur->data);
            cur = cur->next;
        }
        printf("--- 스택의 최하단 ---\n"):
    }
    ```

  - 완성된 스택 사용하기

    ```c
    int main(void){
        Stack stack;
        stack.top = NULL; // 널값을 반드시 넣어줘야 체크 가능
        show(&stack);
        push(&stack, 7);
        push(&stack, 5);
        push(&stack, 4);
        pop(&stack);
        push(&stack, 6);
        pop(&stack);
        show(&stack);
        system("pause");
        return 0;
    }
    ```


> 2019-03-15

### 23강 - 스택을 활용한 계산기 만들기

- 스택을 활용해 수식을 계산하는 방법

  - 수식을 후위 표기법으로 변환한다.
  - 후위 표기법을 계산하여 결과를 도출한다.

- 스택 구현하기

  - 스택의 정의

    ```c
    #define _CRT_SECURE_NO_WARNINGS
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    
    typedef struct Node{
        char data[100];
        struct Node *next;
    } Node;
    
    typedef struct Stack{
        Node *top;
    } Stack;
    ```

  - 스택 함수 구현하기

    ```c
    void push(Stack *stack, char *data){
        Node *node = (Node*)malloc(sizeof(Node));
        strcpy(node->data, data);
        node->next = stack->top;
        stack->top = node;
    }
    
    char* getTop(Stack *stack){
        Node *top = stack->top;
        return top->data;
    }
    
    char* pop(Stack *stack){
        if(stack->top == NULL){
            printf("스택 언더플로우가 발생했습니다. \n");
            return NULL;
        }
        Node *node = stack->top;
        char *data = (char*)malloc(sizeof(char)*100);
        strcpy(data, node->data);
        stack->top = node->next;
        free(node);
        return data;
    }
    ```

- 중위 표기법을 후위 표기법으로 바꾸는 방법

  - 피연산자가 들어오면 바로 출력
  - 연산자가 들어오면 자기보다 우선순위가 높거나 같은 것들을 빼고 자신을 스택에 담는다
  - 여는 괄호 '('를 만나면 무조건 스택에 담는다.
  - 닫는 괄호 ')'를 만나면 '('를 만날 때까지 스택에서 출력한다.

- 후위 표기법으로 변환 

  - 우선순위 함수 만들기

    ```c
    int getPriority(char *i){
        if (!strcmp(i, "(")) return 0;
        if (!strcmp(i, "+") || !strcmp(i, "-")) return 1;
        if (!strcmp(i, "+") || !strcmp(i, "/")) return 2;
        return 3;
    }
    ```

  - 변환 함수 만들기

    ```c
    char* transition(Stack *stack, char **s, int size){
        char res[1000] = "";
        for (int i = 0; i < size; i++){
            if(!strcmp(s[i], "+") || !strcmp(s[i], "-") || !strcmp(s[i], "/")){
                while (stack->top != NULL && getPriority(getTop(stack)) >= getPriority(s[i])){
                    strcat(res, pop(stack)); strcat(res, " ");
                }
                push(stack, s[i]);
            }
            else if(!strcmp(s[i], "(")) push(stack, s[i]);
            else if(!strcmp(s[i], ")")){
                while(strcmp(getTop(stack), "(")){
                    strcat(res, pop(stack)); strcat(res, " ");
                }
            } pop(stack);
        }
        else{strcat(res, s[i]); strcat(res, " "); }
      }
      while(stack->top != NULL){
        strcat(res, pop(stack)); strcat(res, " ");
      }
      return res;
    }
    
    
    
    ```

>2019-03-16

- 어제에 이어서..

- 후위 표기법을 계산하는 방법

  - 피연산자가 들어오면 스택에 담습니다.

  - 연산자를 만나면 스택에서 두 개의 연산자를 꺼내서 연산한 뒤에 그 결과를 스택에 담습니다.

  - 연산을 마친 뒤에 스택에 남아있는 하나의 피연산자가 연산 수행 결과입니다.

    ```c
    void calculate(Stack *stack, char **s, int size){
        int x, y, z;
        for(int i = 0; i<size; i++){
            if(!strcmp(s[i], "+") || !strcmp(s[i], "-") || !strcmp(s[i], "*") || !strcmp(s[i], "/")){
                x = atoi(pop(stack));
                y = atoi(pop(stack));
                if(!strcmp(s[i], "+")) z = y + x;
                if(!strcmp(s[i], "-")) z = y - x;
                if(!strcmp(s[i], "*")) z = y * x;
                if(!strcmp(s[i], "/")) z = y / x;
                char buffer[100];
                sprintf(buffer, "%d", z);
                push(stack, buffer);
            }
            else{
                push(stack, s[i]);
            }
        }
        printf("%s\n", pop(stack));
    }
    ```

    ```c
    int main(void){
        Stack stack;
        stack.top = NULL;
        char a[100] = "( ( 3 + 4 ) * 5 ) - 5 * 7 * 5 - 5 * 10;"
        int size = 1;
        for(int i = 0; i < strlen(a); i++){
            if(a[i] == ' ') size++;
        }
        char *ptr = strtok(a, " ");
        char **input = (char**)malloc(sizeof(char*) * size);
        for (int i = 0; i < size; i++){
            strcpy(input[i], ptr);
            ptr = strtok(NULL, " ");
        }
        char b[1000] = "";
        strcpy(b, transition(&stack, input, size));
        printf("후위 표기법: %s\n", b);
        size = 1;
        for(int i = 0; i < strlen(b)-1; i++){
            if(b[i] == ' ') size++;
        }
        char *ptr2 = strtok(b, " ");
        for(int i = 0; i < size; i++){ // 마지막은 항상 공백이 들어가므로 1을 빼기 
            strcpy(input[i], ptr2);
            ptr2 = strtok(NULL, " ");
        }
        calculate(&stack, input, size);
        system("pause");
        return 0;
    }
    ```


> 2019-03-18

### 24강 - 큐

- 큐(Queue)는 뒤쪽으로 들어가서 앞쪽으로 나오는 자료 구조(Data Structure)입니다.

- 이러한 특성 때문에 스케줄링, 탐색 알고리즘 등에서 다방면으로 활용됩니다.

  - PUSH : 큐에 데이터를 넣습니다.
  - POP : 큐에서 데이터를 빼냅니다.

- 큐의 구현

  - 배열을 이용한 구현방법과 연결 리스트를 이용한 구현방법으로 나뉘어짐

  - 가장 기본적인 형태의 자료구조로 구현 난이도는 낮은 편

  - 배열을 이용한 큐 구현

    - 큐의 선언

      ```c
      #include <stdio.h>
      #define SIZE 10000
      #define INF 9999999
      
      int queue [SIZE];
      int front = 0;
      int rear = 0;
      ```

    - 큐 삽입 함수

      ```C
      void push(int data){
          if(rear >= SIZE){
              printf("큐 오버플로우가 발생했습니다. \n");
              return;
          }
          queue[rear++] = data;
      }
      ```

    - 큐 추출 함수

      ```C
      int pop(){
          if (front == rear){
              printf("큐 언더플로우가 발생했습니다.");
              return -INF;
          }
          return queue[front++];
      }
      ```

    - 큐 전체 출력 함수

      ```c
      void show(){
          printf("--- 큐의 앞 --- \n");
          for(int i = front; i < rear; i++){
              printf("%d\n", queue[i]);
          }
          printf("--- 큐의 뒤 ---\n");
      }
      ```

    - 완성된 큐 사용하기

      ```c
      int main(void){
          push(7);
          push(5);
          push(4);
          pop();
          push(6);
          pop();
          show();
          system("pause");
          return 0;
      }
      ```

  - 연결 리스트를 이용한 큐 구현

    - 큐의 선언

      ```c
      #include <stdio.h>
      #include <stdlib.h>
      #define INF 99999999
      
      typedef struct{
          int data;
          struct Node *next;
      } Node;
      
      typedef struct{
          Node *front;
          Node *rear;
          int count;
      } Queue;
      ```

    - 큐 삽입 함수

      ```c
      void push(Queue *queue, int data){
          Node *node = (Node*)malloc(sizeof(Node));
          node->data = data;
          node->next = NULL;
          if(queue->count == 0){
              queue->front = node;
          }
          else{
              queue->rear->next = node;
          }
          queue->rear = node;
          queue->count++;
      }
      ```

    - 큐 추출 함수

      ```c
      int pop(Queue *queue){
          if(queue->count == 0){
              printf("큐 언더플로우가 발생했습니다.\n");
              return -INF;
          }
          Node *node = queue->front;
          int data = node->data;
          queue->front = node->next;
          free(node);
          queue->count--;
          return data;
      }
      ```

    - 큐 전체 출력 함수

      ```c
      void show(Queue *queue){
          Node *cur = queue->front;
          printf("--- 큐의 앞 ---\n");
          while(cur != NULL){
              printf("%d\n", cur->data);
              cur = cur->next;
          }
          printf("--- 큐의 뒤 ---\n");
      }
      ```

    - 완성된 큐 사용하기

      ```c
      int main(void){
          Queue queue;
          queue.front = queue.rear = NULL;
          queue.count = 0;
          push(&queue, 7);
          push(&queue, 5);
          push(&queue, 4);
          pop(&queue);
          push(&queue, 6);
          pop(&queue);
          show(&queue);
          system("pause");
          return 0;
      }
      ```




> 2019-03-20

### 25강 - 선택 정렬과 삽입 정렬

- 선택정렬

  - 선택 정렬이란 **가장 작은 것을 선택해서 앞으로 보내는 정렬 기법**입니다. 가장 작은 것을 선택하는 데에 N번, 앞으로 보내는 데에 N번의 연산으로 O(N^2)의 시간 복잡도를 가집니다.

  - 배열 선언

    ```c
    #define _CRT_SECURE_NO_WARINGS
    #include <stdio.h>
    #include <limits.h>
    #define SIZE 1000
    
    int a[SIZE];
    
    int swap(int *a, int *b){
        int temp = *a;
        *a = *b;
        *b = temp;
    }
    ```

  - 선택 정렬 수행하기

    ```c
    int main(void){
        int n, min, index;
        scanf("%d", &n);
        for(int i = 0; i < n; i++) scanf("%d", &a[i]);
        for(int i = 0; i < n; i++){
            min = INT_MAX;
            for(int j = i; j < n ; j++){
                if(min > a[j]){
                    min = a[j];
                    index = j;
                }
            }
            swap(&a[i], &a[index]);
        }
        for(int i = 0; i < n; i++) printf("%d ", a[i]);
        system("pause");
        return 0;
    }
    ```

- 삽입정렬

  - 삽입 정렬이란 **각 숫자를 적절한 위치에 삽입하는 정렬 기법**이다. 들어갈 위치를 선택하는 데에 N번, 선택하는 횟수로 N번이므로 O(N^2)의 시간 복잡도를 가진다. **선택정렬보다 약간 더 빠르게 동작한다**

  - 배열 선언

    ```c
    #define _CRT_SECURE_NO_WARINGS
    #include <stdio.h>
    #define SIZE 1000
    
    int a[SIZE];
    
    int swap(int *a, int *b){
        int temp = *a;
        *a = *b;
        *b = temp;
    }
    ```

  - 삽입 정렬 수행하기

    ```c
    int main(void){
        int n;
        scanf("%d", &n);
        for(int i = 0; i < n; i++) scanf("%d", &a[i]);
        for(int i = 0; i < n - 1; i++){
            int j = i;
            while(j >= 0 && a[j] > a[j + 1]){
                swap(&a[j], &a[j + 1]);
                j--;
            }
        }
        for(int i = 0; i < n; i++) printf("%d ", a[i]);
        system("pause");
        return 0;
    }
    ```

- 선택 정렬과 삽입 정렬은 비효율적이지만 가장 간단한 알고리즘이다.

> 2019-03-25

### 26강  -  퀵정렬

- 퀵정렬

  - 퀵정렬이란 피벗을 기준으로 큰 값과 작은 값을 서로 교체하는 정렬 기법. 값을 서로 교체하는 데에 N번, 엇갈린 경우 교체 이후에 원소가 반으로 나누어지므로 전체원소를 나누는 데에 평균적으로 logN번이 소요되므로 평균적으로 θ(NlogN)의 시간 복잡도를 가진다.

  - 원소를 절반씩 나눌 때 logN의 시간 복잡도가 나오는 대표적인 예시는 완전 이진 트리입니다. 이러한 완전 이진 트리 형태는 흔히 컴퓨터 공학에서 가장 선호하는 이상적인 형태입니다.

  - 배열선언

    ```c
    #define _CRT_SECURE_NO_WARNINGS
    #include <stdio.h>
    #define SIZE 1000
    
    int a[SIZE];
    
    int swap(int *a, int *b){
        int temp = *a;
        *a = *b;
        *b  = temp;
    }
    ```

  - 퀵 정렬 구현

    ```c
    void quickSort(int start, int den){
        if(start >= end) return;
        int key = start, i = start + 1, j = end, temp;
        while(i <= j){ //엇갈릴 떄까지 반복
        	while(i <= end && a[i] <= a[key]) i++;
        	while(j > start && a[j] >= a[key]) j--;
        	if(i > j)swap(&a[key], &a[j]);
        	else swap(&a[i], &a[j]);
        }
        quickSort(start, j-1);
        quickSort(j+1, end);
    }
    
    int main(void){
        int n;
        scanf("%d", &n);
        for(int i = 0; i < n; i++) scanf("%d", &a[i]);
        quickSort(0, n - 1);
        for(int i = 0; i < n; i++) printf("%d", a[i]);
        system("pause");
        return 0;
    }
    ```

  - 퀵 정렬은 편향된 분할이 발생할 때 연산의 양이 O(N^2)입니다. 따라서 실제로 정렬을 함에 있어서는 퀵 정렬을 직접 구현하지 않습니다. 따라서 C++의 Algorithm 라이브러리를 사용합니다. Algorithm 라이브러리의 sort() 함수는 퀵 정렬을 기반으로 하되 O(NlogN)을 보장합니다.

- 정리

  - 퀵 정렬은 평균적인 시간 복잡도가 O(NlogN)인 가장 보편적인 정렬 알고리즘이다. 

>  2019-03-27

### 27강 - 계수 정렬

- 계수 정렬(Counting Sort)는 크기를 기준으로 데이터의 개수를 세는 정렬 알고리즘이다. 각 데이터를 바로 크기를 기준으로 분류하므로 O(N)의 시간 복잡도를 가진다.

- 차례대로 원소의 개수만큼 출력 : 0 0 1 1 1 2 2 2 3 3

- ```C
  #define _CRT_SECURE_NO_WARNINGS
  #include <stdio.h>
  #define MAX_VALUE 10001
  
  int n, m;
  int a[MAX_VALUE];
  
  int mail(){
      scanf("%d", &n);
      for(int i = 0; i < n; i++){ scanf("%d", &m); a[m]++; }
      for(int i = 0; i < MAX_VALUE; i++){
          while(a[i] != 0){ printf("%d ", i); a[i]--;}
      }
      system("pause");
  }
  ```

- 계수 정렬은 시간 복잡도가 O(N)인 정렬 알고리즘

- 데이터의 크기가 한정적일 때 사용가능

> 2019-04-06

### 28강 - 기수 정렬

- 기수 정렬(Radix Sort)는 자릿수를 기준으로 차례대로 데이터를 정렬하는 알고리즘입니다. 각 데이터를 **자릿수를 기준으로 분류**하므로 가장 큰 자릿수를 D라고 했을 때 O(DN)의 시간 복잡도를 가집니다.
  - D가 10이 넘어가려면 데이터 수는 10억이 넘어야 한다 → 따라서 보통 N에 가까운 시간복잡도를 가진다.

```C
#define _CRT_SECURE_NO_WARNNGS
#include <stdio.h>
#define MAX 10000

void radixSort(int *a, int n){
    int res[MAX], maxValue = 0;
    int exp = 1;
    for (int i = 0; i < n; i++){
        if(a[i] > maxValue) maxValue = a[i];
    }
    while (maxValue / exp > 0) { // 1의 자리부터 계산
    int bucket[10] = {0};
    for(int i = 0; i < n; i++) bucket[a[i] / exp % 10]++; //자릿수 배열 처리
    for(int i = 1; i < 10; i++) bucket[i] += bucket[i -1]; //누적 계산
        for(int i = n - 1; i >=0; i++){//같은 자릿수끼리는 순서를 유지
            res[--bucket[a[i]] / exp % 10]] = a[i];
        }
        for(int i = 0; i < n; i++) a[i] = res[i]; //기본 배열 갱신
        exp *= 10;
    }
}

int main(void){
    int a[MAX];
    int i, n;
    scanf("%d", &n);
    for(int i = 0; i < n; i++){
        scanf("%d", &a[i]);
    }
    radixSort(a, n);
    for(int i = 0; i < n; i++){
        printf("%d ", a[i]);
    }
    system("pause");
}
```











<!--stackedit_data:
eyJoaXN0b3J5IjpbNDgwMTgzOTcyXX0=
-->