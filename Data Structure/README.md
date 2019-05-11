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

- 기수 정렬은 시간 복잡도가 O(DN)인 정렬 알고리즘입니다.
- 기수 정렬은 계수 정렬보다 약간 더 느리지만, 숫자가 매우 큰 상황에서도 사용할 수 있습니다.


> 2019-04-14

### 29강 - 이진트리

- 트리는 나무의 형태를 뒤집은 것과 같은 형태의 자료구조.
- 부모, 자식, 형제 노드 구조를 가짐.
- 길이(Length)란 출발 노드에서 목적지 노드까지 거쳐야 하는 가짓수를 의미
- 깊이(Depth)란 루트 노드에서 특정 노드까지의 길이를 의미한다.
- 높이(Height)란 루트 노드에서 가장 깊은 노드까지의 길이
- 이진 트리는 최대 2개의 자식을 가질 수 있는 트리
- 포화 이진트리(Full Binary Tree) 리프 노드를 제외한 모든 노드가 두 자식을 가지고 있는 트리
- 완전 이진트리(Complete Binary Tree)는 모든 노드들이 외쪽 자식부터 차근차근 채워진 노드
- 높이 균형트리(Height Balanced Tree)는 왼쪽 자식 트리와 오른쪽 자식 트리의 높이가 1 이상 차이 나지 않는 트리
- 이진트리는 많은 양의 노드를 낮은 높이에서 관리할 수 있다는 점에서 데이터 활용의 효율성이 높아진다.
- 데이터 저장, 탐색 등의 다양한 목적에서 사용할 수 있다.

> 2019-04-15

### 30강 이진 트리의 구현 및 순회

- 이진 트리는 포인터를 이용하여 구현하면 효과적인 데이터 관리가 가능합니다.

  ```c
  #include <stdio.h>
  #include <stdlib.h>
  
  typedef struct {
      int data;
      struct Node *leftChild;
      struct Node *rightChild;
  } Node;
  
  Node* initNode(int data, Node* leftChild, Node* rightChild){
      Node* node = (Node*)malloc(sizeof(Node));
      node->data = data;
      node->leftChild = leftChild;
      node->rightChild = rightChild;
      return node;
  }
  ```

- 이진 트리의 순회
  : 이진 트리에 담긴 데이터를 하나씩 방문하는 방법으로는 대표적으로 세 가지가 있습니다.

- 이진 트리의 전위 순회

  - 자기 자신을 출력합니다.
  - 왼쪽 자식을 방문합니다.
  - 오른쪽 자신을 방문합니다.

  ```c
  void preorder(Node* root){
      if(root){
          printf("%d ", root->data);
          preorder(root->leftChild);
          preorder(root->rightChild);
      }
  }
  ```

- 이진 트리의 중위 순회

  - 왼쪽 자식을 방문합니다.
  - 자기 자신을 출력합니다.
  - 오른쪽 자식을 방문합니다.

  ```c
  void inorder(Node* root){
      if(root){
          inorder(root->leftChild);
          printf("%d ", root->data);
          inorder(root->rightChild);
      }
  }
  ```

- 이진 트리의 후위 순회

  - 왼쪽 자식을 방문합니다.
  - 오른쪽 자식을 방문합니다.
  - 자기 자신을 출력합니다. → 루트를 마지막으로 출력

  ```c
  void postorder(Node* root){
      if(root){
          postorder(root->leftChild);
          postorder(root->rightChild);
          printf("%d ", root->data);
      }
  }
  ```

- 이진 트리의 구현 및 순회

  - 이진 트리 사용해보기

    ```c
    int main(void){
        Node* n7 = initNode(50, NULL, NULL);
        Node* n6 = initNode(37, NULL, NULL);
        Node* n5 = initNode(23, NULL, NULL);
        Node* n4 = initNode(5, NULL, NULL);
        Node* n3 = initNode(48, n6, n7);
        Node* n2 = initNode(17, n4, n5);
        Node* n1 = initNode(30, n2, n3);
        preorder(n1);
        printf("\n");
        inorder(n1);
        printf("\n");
        postorder(n1);
        printf("pause");
        return 0;
    }
    ```


> 2019-04-16

### 31강 - 우선순위 큐

- 우선순위 큐는 '우선순위'를 가진 데이터를 저장하는 큐를 의미합니다. 데이터를 꺼낼 때 우선 순위가  가장 높은 데이터가 가장 먼저 나온다는 특징이 있어 많이 활용되고 있습니다.

- 우선순위 큐는 운영체제의 작업 스케줄링, 정렬, 네트워크 관리 등의 다양한 기술에 적용되고 있습니다. 

- 우선순위 큐와 큐의 차이점
  : 일반적인 형태의 큐는 선형적인 형태를 가지고 있지만 우선순위 큐는 트리(Tree) 구조로 보는 것이 합리적입니다. 일반적으로 우선순위 큐는 **최대 힙**을 이용해 구현함.

- 최대 힙(Max Heap)

  - 최대 힙은 부모 노드가 자식 노드보다 값이 큰 완전 이진 트리를 의미

  - 최대 힙의 루트 노드는 전체 트리에서 가장 큰 값을 가진다는 특징이 있다.

  - 우리는 항상 전체 트리가 최대 힙 구조를 유지하도록 자료구조를 만들 수 있다.

    - PUSH : 우선순위 큐에 데이터를 삽입한다.
    - POP : 우선순위 큐에서 데이터를 추출한다.

  - 우선순위 큐의 삽입

    - 삽입할 원소는 완전 이진 트리를 유지하는 형태로 순차적으로 삽입된다.(왼쪽부터 오른쪽으로 채워간다)
    - 삽입 이후에는 루트 노드까지 거슬러 올라가면서 최대 힙을 구성한다 (상향식)

  - 우선순위 큐의 삭제

    - 삭제를 할 때는 루트 노드를 삭제하고, 가장 마지막 원소를 루트 노드의 위치로 옮겨줍니다.
    - 삭제 이후에는 리프 노드까지 내려가면서 최대 힙을 구성합니다. (하향식)

  - 우선순위 큐의 정의

    ```c
    #define _CRT_SECURE_NO_WARNINGS
    #include <stdio.h>
    #define MAX_SIZE 10000
    
    void swap(int *a, int *b){
        int temp = *a;
        *a = *b;
        *b = temp;
    }
    
    typedef struct{
        int heap[MAX_SIZE];
        int count;
    } priorityQueue;
    ```

  - 우선순위 큐의 삽입

    ```c
    void push(priorityQueue *pq, int data){
        if(pq->count >= MAX_SIZE) return;
        pq->heap[pq->count] = data;
        int now = pq->count;
        int parent = (pq->count - 1) / 2;
        // 새 원소를 삽입한 이후에 상향식으로 힙을 구성합니다.
        while(now > 0 && pq->heap[now] > pq->heap[parent]){
            swap(&pq->heap[now], &pq->heap[parent]);
            now = parent;
            parent = (parent - 1) / 2;
        }
        pq->count++;
    }
    ```

  - 우선순위 큐의 추출

    ```c
    int pop(priorityQueue *pq){
        if (pq->count <= 0) return -9999;
        int res = pq->heap[0];
        pq->count--;
        pq->heap[0] = pq->heap[pq->count];
        int now = 0, leftChild = 1, rightChild = 2;
        int target = now;
        // 새 원소를 추출한 이후에 하향식으로 힙을 구성합니다.
        while (leftChild < pq->count){
            if (pq->heap[target] < pq->heap[leftChild]) target = leftChild;
            if (pq->heap[target] < pq->heap[rightChild] && rightChild < pq->count) target = rightChild;
            if (target == now) break; // 더 이상 내려가지 않아도 될 때 종료
            else{
                swap(&pq->heap[now], &pq->heap[target]);
                now = target;
                leftChild = now * 2 + 1;
                rightChild = now * 2 + 2;
            }
        }
        return res;
    }
    ```

  - 우선순위 큐의 사용

    ```c
    int main(void){
        int n, data;
        scanf("%d", &n);
        priorityQueue pq;
        pq.count = 0;
        for (int i = 0; i < n; i++){
            scanf("%d", &data);
            push(&pq, data);
        }
        for (int i = 0; i < n; i++){
            int data = pop(&pq);
            printf("%d ", data);
        }
        system("pause");
        return 0;
    }
    ```

  - 우선순위 큐는 완전 이진 트리 형태의 힙을 이용해 구현할 수 있습니다.

  - 우선순위 큐의 삽입과 삭제는 O(logN)의 시간 복잡도를 가집니다.

  - 따라서 우선순위 큐를 이용한 정렬은 O(NlogN)의 시간 복잡도를 가집니다.


> 2019-04-19

### 32강 - 순차 탐색과 이진 탐색

- 순차 탐색(Sequential Search)은 특정한 원소를 찾기 위해 원소를 순차적으로 하나씩 탐색하는 방법

- 문자열 순차 탐색 구현 1)

  ```c
  #define _CRT_SECURE_NO_WARNINGS
  #include <stdio.h>
  #include <stdlib.h>
  #include <string.h>
  #define LENGTH 1000
  
  char **array;
  int founded;
  ```

- 문자열 순차 탐색 구현 2)

  ```c
  int main(void){
      int n;
      char *word;
      word = malloc(sizeof(char) * LENGTH);
      scanf("%d %s", &n, word);
      array = (char**) malloc(sizeof(char*) * n);
      for(int i = 0; i < n; i++){
          array[i] = malloc(sizeof(char) * LENGTH);
          scanf("%s", array[i]);
      }
      for(int i = 0; i < n; i++){
          if(!strcmp(array[i], word)){
              printf("%d번째 원소입니다. \n", i + 1);
              founded = 1;
          }
      }
      if (!founded) printf("원소를 찾을 수 없습니다. \n");
      system("pause");
      return 0;
  }
  ```

  - 순차 탐색(Sequential Search)은 데이터 정렬 유무에 상관없이 가장 앞에 있는 원소부터 하나씩 확인해야 한다는 점에서 O(N)의 시간 복잡도를 가집니다.

  - 이진 탐색(Binary Search)은 배열 내부 데이터가 이미 정렬 되어 있는 상황에서 사용 가능한 알고리즘입니다. 탐색 범위를 절반씩 좁혀가며 데이터를 탐색하는 특징이 있습니다.

  - 이진 탐색(Binary Search)는 한 번 확인할 때마다 보아야 하는 원소의 개수가 절반씩 줄어든다는 점에서 탐색 시간이 O(logN)의 시간 복잡도를 가집니다.

  - 이진 탐색 정의

    ```c
    #define _CRT_SECURE_NO_WARNINGS
    #include <stdio.h>
    #define MAX_SIZE 100000
    
    int a[MAX_SIZE];
    int founded = 0;
    
    int search(int start, int end, int target){
        if(start > end) return -9999;
        int mid = (start + end) / 2;
        if(a[mid] == target) return mid;
        else if (a[mid] > target) return search(start, mid - 1, target);
        else return search(mid + 1, end, target);
    }
    
    int main(void){
        int n, target;
        scanf("%d %d", &n, &target);
        for(int i = 0; i < n; i++) scanf("%d", &a[i]);
        int result = search(0, n - 1, target);
        if(result != -9999) printf("%d번째 원소입니다. \n", result + 1);
        else printf("원소를 찾을 수 없습니다. \n");
        system("pause");
        return 0;
    }
    ```

- 이진 탐색(Binary Search)는 한 번 확인할 때마다 보아야 하는 원소의 개수가 절반씩 줄어든다는 점에서 탐색 시간에서 O(logN)의 시간 복잡도를 가집니다.

### 33강 - 그래프의 개념과 구현

- 그래프(Graph)란 사물을 정점(Vertex)와 간선(Egde)으로 나타내기 위한 도구

- 다음의 두가지 방식으로 구현할 수 있음

  - 인접 행렬(Adjacency Matrix) : 2차원 배열을 사용하는 방식
  - 인접 리스트(Adjacency List) : 리스트를 사용하는 방식

- 인접 행렬에서는 그래프를 2차원 배열로 표현합니다.

- 무방향 비가중치 그래프와 인접 행렬

  - 모든 간선이 방향성을 가지지 않는 그래프를 무방향 그래프라고 합니다.

  - 모든 간선에 가중치가 없는 그래프를 비가중치 그래프라고 합니다.

  - 무방향 비가중치 그래프가 주어졌을 때 연결되어 있는 상황을 인접 행렬로 출력할 수 있습니다.

    ```c
    #define _CRT_SECURE_NO_WARNINGS
    #include <stdio.h>
    
    int a[1001][1001];
    int n, m;
    
    int main(void){
        scanf("%d %d", &n, &m);
        for(int i = 0; i < m; i++){
            int x, y;
            scanf("%d %d", &x. &y);
            a[x][y] = 1;
            a[y][x] = 1;
        }
        for (int i = 1; i <= n; i++){
            for(int j = 1; j <= n; j++){
                printf("%d ", a[i][k]);
            }
            printf("\n");
        }
        system("pause");
    }
    ```

- 방향 가중치 그래프와 인접 리스트

  - 모든 간선이 방향을 가지는 그래프를 방향 그래프라고 한다.

  - 모든 간선에 가중치가 있는 그래프를 가중치 그래프라고 한다.

  - 방향 가중치 그래프가 주어졌을 때 연결되어 있는 상황을 인접 리스트로 출력할 수 있다.

  - 1) 연결 리스트 구조체 만들기

    ```c
    #define _CRT_SECURE_NO_WARNINGS
    #include <stdio.h>
    #include <stdlib.h>
    
    typedef struct{
        int index;
        int distance;
        struct Node *next;
    } Node;
    ```

  - 2) 연결 리스트 삽입 함수 만들기

    ```c
    void addFront(Node *root, int index, int distance){
        Node *node = (Node*)malloc(sizeof(Node));
        node->index = index;
        node->distance = distance;
        node->next = root->next;
        root->next = node;
    }
    ```

  - 3) 연결 리스트 출력 함수

    ```c
    void showAll(Node *root){
        Node *cur = root->next;
        while(cur != NULL){
            printf("%d"(거리 : %d) ", cur->index, cur->distance);
            cur = cur->next;
        }
    }
    ```

  - 4) 연결 리스트 사용하기

    ```c
    int main(void){
        int n, m;
        scanf("%d %d", &n, &m);
        Node** a = (Node*)malloc(sizeof(Node*) * (n + 1));
        for(int i = 1; i <= n; i++){
            a[i] = (Node*)malloc(sizeof(Node));
            a[i]->next = NULL;
        }
        for(int i = 0; i < m; i++){
            int x, y distance;
            scanf("%d %d %d", &x, &y, &distance);
            addFront(a[x], y, distance);
        }
        for(int i = 1; i <= n; i++){
            printf("원소 [%d]: ", i);
            showAll(a[i]);
            printf("\n");
        }
        system("pause");
        return 0;
    }
    ```

  - 인접 행렬은 모든 정점들의 연결 여부를 저장하여 O(V^2)의 공간을 요구하므로 공간 효율성이 떨어지지지만 두 정점이 서로 연결되어 있는지 확인하기 위해 O(1)의 시간을 요구합니다.

  - 인접 리스트는 연결된 간선의 정보만을 저장하여 O(E)의 공간을 요구하므로 공간 효율성이 우수하지만 두 정점이 서로 연결되어 있는지 확인하기 위해 O(V)의 시간을 요구합니다. 

> 2019-04-20

### 34강 - 깊이 우선 탐색

- 깊이 우선 탐색(Depth First Search)은 탐색을 함에 있어서 보다 깊은 것을 우선적으로 하여 탐색하는 알고리즘. 깊이 우선 탐색은 기본적으로 전체 노드를 맹목적으로 탐색하고자 할 때 사용. 깊이 우선 탐색 알고리즘은 스택(Stack) 자료구조에 기초한다.

- 깊이 우선탐색음 빠르게 모든 경우의 수를 탐색하고자 할 때 쉽게 탐색할 수 있다.

- 알고리즘 순서

  1. 탐색 시작 노드를 스택에 삽입하고 방문 처리한다.
  2. 스택의 최상단 노드에서 방문하지 않은 인접 노드가 하나라도 있으면 그 노드를 스택에 넣고 **방문 처리**를 한다. 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼낸다.
  3. 2번의 과정을 더 이상 수행할 수 없을 때까지 반복한다.

- 깊이 우선 탐색 알고리즘은 스택(Stack) 자료구조에 기초한다는 점에서 구현이 간단하다. 실제로는 스택을 쓰지 않아도 되며 탐색을 수행함에 있어서 O(N)의 시간이 소요된다.

- 1) 연결리스트 정의

  ```c
  #define _CRT_SECURE_NO_WARNINGS
  #include <stdio.h>
  #include <stdlib.h>
  #define MAX_SIZE 1001
  
  typedef struct{
      int index;
      struct Node *next;
  } Node;
  
  Node** a;
  int n, m, c[MAX_SIZE];
  ```

- 2) 연결 리스트 삽입 함수

  ```c
  void addFront(Node *root, int index){
      Node *node = (Node*)malloc(sizeof(Node));
      node->index = index;
      node->next = root->next;
      root->next = node;
  }
  ```

- 3) 깊이 우선 탐색 함수

  ```c
  void dfs(int x){
      if (c[x]) return;
      c[x] = 1;
      printf("%d ", x);
      Node *cur = a[x]->next;
      while (cur != NULL){
      	int next = cur->index;
      	dfs(next);
      	cur = cur->next;
      }
  }
  ```

- 4) 깊이 우선 탐색 이용해보기

  ```c
  int main(void){
      scanf("%d %d", &n, &m);
      a = (Node**)malloc(sizeof(Node*) * MAX_SIZE);
      for (int i = 1; i <= n; i++){
          a[i] = (Node*)malloc(sizeof(Node));
          a[i]->next = NULL;
      }
      for (int i = 0; i < m; i++){
          int x, y;
          scanf("%d %d", &x, &y);
          addFront(a[x], y);
          addFront(a[y], x);
      }
      dfs(1);
      system("pause");
      return 0;
  }
  ```

- 깊이 우선 탐색은 O(N)의 시간이 소요되는 전수 탐색 알고리즘이다.

### 35강 - 너비 우선 탐색

- 너비 우선 탐색(Breath First Search)은 너비를 우선으로 하여 탐색을 수행하는 탐색 알고리즘이다. DFS와 마찬가지로 맹목적으로 전체 노드를 탐색하고자 할 때 자주 사용되며 큐(Queue) 자료구조에 기초한다.

- 너비 우선 탐색은 고급 그래프 탐색 알고리즘에서 자주 활용되므로 고급 개발자가 되기 위해서는 너비 우선 탐색에 대해 숙지해야 한다.

- 알고리즘 동작원리

  1. 탐색 시작 노드를 큐에 삽입하고 방문처리 한다
  2. 큐에서 노드를 꺼내 해당 노드의 인접 노드 중에서 방문하지 않은 노드들을 모두 큐에 삽입하고, 방문 처리 한다.
  3. 2번의 과정을 더 이상 수행할 수 없을 때까지 반복한다.

- 너비 우선 탐색 알고리즘은 큐(Queue) 자료구조에 기초한다는 점에서 구현이 간단하다. 실제로 구혐함에 있어 큐 STL을 사용하면 좋으며 탐색을 수행함에 있어서 O(N)의 시간이 소요된다. 일반적인 경우 실제 수행 시간은 DFS보다 좋은 편이다.

- 1) 연결 리스트 정의

  ```c
  #define _CRT_SECURE_NO_WARNINGS
  #include <stdio.h>
  #inclue <stdlib.h>
  #define INF 9999999
  #define MAX_SIZE 1001
  
  typedef struct{
  	int index;
      struct Node *next;
  } Node;
  
  typedef struct{
      Node *front;
      Node *rear;
      int count;
  } Queue;
  
  Node** a;
  int n, m, c[MAX_SIZE];
  ```

- 2) 연결 리스트 삽입 함수

  ```c
  void addFront (Node *root, int index){
      Node *node = (Node*)malloc(sizeof(Node));
      node->index = index;
      node->next = root->next;
      root->next = node;
  }
  ```

- 3) 큐 삽입 함수

  ```c
  void queuePush(Queue *queue, int index){
      Node *node = (Node*)malloc(sizeof(Node));
      node->index = index;
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

- 4) 큐 추출 함수

  ```c
  int queuePop(Queue *queue){
      if (queue->count == 0){
          printf("큐 언더플로우가 발생했습니다. \n");
          return -INF;
      }
      Node *node = queue->front;
      int index = node->index;
      queue->front = node->next;
      free(node);
      queue->count--;
      return index;
  }
  ```

- 5) 너비 우선 탐색 함수

  ```c
  void bfs(int start){
      Queue q;
      q.front = q.rear = NULL;
      q.count = 0;
      queuePush(&q, start);
      c[start] = 1;
      while (q.count != 0){
          int x = queuePop(&q);
          printf("%d ", x);
          Node *cur = a[x]->next;
          while (cur != NULL){
              int next = cur->index;
              if(!c[next]){
                  queuePush(&q, next);
                  c[next] = 1;
              }
              cur = cur->next;
          }
      }
  }
  ```

- 6) 너비 우선 탐색 이용해보기

  ```c
  int main(void){
      scanf("%d %d", &n, &m);
      a = (Node**)malloc(sizeof(Node*) * (MAX_SIZE));
      for(int i = 1; i <= n; i++){
          a[i] = (Node*)malloc(sizeof(Node));
          a[i]->next = NULL;
      }
      for(int i = 0; i < m; i++){
          int x, y;
          scanf("%d %d", &x, &y);
          addFront(a[x], y);
          addFront(a[y], x);
      }
      bfs(1);
      system("pause");
      return 0;
  }
  ```

- 너비 우선 탐색은 O(N)의 시간이 소요되는 전수 탐색 알고리즘이다. → 깊이 우선 탐색보다 구현시간이 다소 빠르다. ??

> 2019-04-24

### 36강 - 이진 탐색 트리

- 이진 탐색 트리에서는 항상 부모 노드가 왼쪽 자식보다는 크고, 오른쪽 자식보다는 작다.

- 이진 탐색 트리(Binary Search Tree)에서는 한번 확인할 때마다 보아야 하는 원소의 개수가 절반씩 줄어든다는 점에서 '완전 이진 트리'인 경우 탐색 시간에 O(logN)의 시간 복잡도를 가진다.

- 이진 탐색 트리에서 탐색을 할 때는 찾고자 하는 값이 부모 노드보다 작을 경우 왼쪽 자식으로, 찾고자 하는 값이 부모 노드보다 클 경우 오른쪽 자식으로 이어 나가면서 방문한다.

- 이진 탐색 트리의 정의

  ```c
  #include <stdio.h>
  #include <stdlib.h>
  
  typedef struct{
  	int data;
  	struct Node* leftChild;
  	struct Node* rightChild;
  } Node;
  ```

- 이진 탐색 트리의 삽입

  ```c
  Node* insertNode(Node* root, int data){
      if(root == NULL){
          root = (Node*)malloc(sizeof(Ndoe));
          root->leftChild = root->rightChild = NULL;
          root->data = data;
          return root;
      }
      else{
          if(root->data > data){
              root->leftChild = insertNode(root->leftChild, data);
          }
          else{
              root->rightChild = insertNode(root->rightChild, data);
          }
      }
          return root;
  }
  ```

- 이진 탐색 트리의 탐색

  ```c
  Node* searchNode(Node* root, int data){
  	if (root == NULL) return NULL;
      if (root->data == data) return root;
      else if (root->data > data) return searchNode(root->leftChild, data);
      else return searchNode(root->rightChild, data);
  }
  ```

- 이진 탐색 트리의 순회

  ```c
  void preorder(Node* root){
  	if (root == NULL) return;
      printf("%d ", root->data);
      preorder(root->leftChild);
      preorder(root->rightChild);
  }
  ```

- 이진 탐색 트리 이용해보기

  ```c
  int main(void){
  	Node* root = NULL;
      root = insertNode(root, 30);
      root = insertNode(root, 17);
      root = insertNode(root, 48);
      root = insertNode(root, 5);
      root = insertNode(root, 23);
      root = insertNode(root, 37);
      root = insertNode(root, 50);
      preorder(root);
      system("pause");
  }
  ```

- 이진 탐색 트리의 삭제

  - 1) 자식이 없는 경우 
    삭제할 노드의 자식이 없는 경우 단순히 제거하면 된다.
  - 2) 자식이 하나만 존재하는 경우
    삭제할 노드의 자식이 하나만 존재하는 경우 삭제할 노드의 자리에 자식 노드를 넣는다. 
  - 3) 자식이 둘 다 존재하는 경우
    자식이 둘 다 존재하는 경우 그 다음으로 삭제할 노드의 자리에 자기 다음으로 큰 노드를 넣는다. 

- 이진 탐색 트리의 가장 작은 원소 찾기 함수

  ```c
  Node* findMinNode(Node* root){
  	Node* node = root;
      while (node->leftChild != NULL){
          node = node->leftChild;
      }
      return node;
  }
  ```

- 이진 탐색 트리의 삭제 함수

  ```c
  Node* deleteNode(Node* root, int data){
  	Node* node = NULL;
  	if (root == NULL) return NULL;
  	if (root->data > data) root->leftChild = deleteNode(root->leftChild, data);
  	else if (root->data < data) root->rightChild = deleteNode(root->rightChild, data);
  	else{
  		if(root->leftChild != NULL && root->rightChild != NULL){
  		node = findMinNode(root->rightChild);
  		root->data = node->data;
  		root->rightChild = deleteNode(root->rightChild, node->data);
  		}
  		else{
  			node = (root->leftChild != NULL) ?root-> leftchild : root->rightChild;
  			free(root);
  			return node;
  		}
  	}
  	return root;
  }
  ```

- 이진 탐색 트리의 성능을 최대로 끌어내기 위해서는 이진 탐색 트리각 완전 이진 트리에 가까워 질 수 있도록 설계해야 한다. 
- 완전 이진 트리(Complete Binary Tree)란 데이터가 루트(Root) 노드부터 시작해서 자식 노드가 왼쪽 자식 노드, 오른쪽 자식 노드로 차례대로 들어가는 구조의 이진 트리이다. 
- 트리의 효율성
  
  - 트리(Tree)를 사용하면 데이터를 처리함에 있어서 효율적이다. 트리에서 데이터의 개수가 N개일 때 배열과 마찬가지로 O(N)의 공간만이 소요되며 삽입 및 삭제에 있어서 일반적인 경우 기존의 배열(Array)를 이용하는 방식보다 효율적이다. 그래서 데이터베이스 등 대용량 저장 및 검색 자료구조로 많이 활용된다. 
- 정상적으로 설계된 완전 이진 트리(Complete Binary Tree)에서는 어떠한 원소라도 탐색함에 있어서 O(logN)의 시간이 소요된다.
- 반면에 한쪽으로 치우친 편향 이진 트리(Skewed Binary Tree)의 경우 탐색에 있어 O(N)의 시간 복잡도가 형성되므로 기존의 배열(Array)을 사용하는 것보다 오히려 많은 공간과 시간이 낭비된다.
- 따라서 이진 트리(Binary Tree)를 만들 때는 트리의 균형이 맞도록 설정하는 것이 중요하다.
- 요약
  - 편향 이진 트리(Skewed Binary Tree)의 경우 탐색에 있어 O(N)의 시간 복잡도를 가진다.
  - 따라서 이진 탐색 트리를 최대한 완전 이진 트리의 형태를 유지할 수 있도록 해야한다.

>2019-04-27

### 37강 - AVL 트리

- AVL 트리는 균형이 갖춰진 이진 트리(Binary Tree)를 의미

- 완전 이진 트리는 검색에 있어서 O(logN)의 시간 복잡도를 유지할 수 있음

- AVL 트리는 간단한 구현 과정으로 특정 이진 트리가 완전 이진 트리에 가까운 형태를 유지하도록 해준다.

- AVL 트리는 균형 인수(Balance Factor)라는 개념을 이용한다.

  - 균형 인수 = |왼쪽 자식 높이 - 오른쪽 자식 높이 |
  - -2 이상인지 2이하인지 보고 균형을 맞추는 작업을 한다.

- AVL 트리는 모든 노드에 대한 균형 인수가 +1, 0, -1인 트리를 의미한다.

- 균형 인수가 위 세 가지 경우에 해당하지 않는 경우 '회전(Rotation)'을 통해 트리를 재구성해야 한다.

- AVL 트리는 총 4가지 형식에 의하여 균형이 깨질 수 있다. 균형 인수가 깨지는 노드를 X라고 했을 때 4가지 형식은 다음과 간다.

  1. LL 형식 : X의 왼쪽 자식의 왼쪽에 삽입하는 경우
  2. LR 형식 : X의 왼쪽 자식의 오른쪽에 삽입하는 경우
  3. RR 형식 : X의 오른족 자식의 오른쪽에 삽입하는 경우
  4. RL 형식 : X의 오른쪽 자식의 왼쪽에 삽입하는 경우

- AVL 트리의 각 노드는 '균형 인수'를 계산하기 위한 목적으로 자신의 '높이(Height)' 값을 가진다.

- AVL 트리의 정의

  ```c
  #include <stdio.h>
  #include <stdlib.h>
  
  int getMax(int a, int b){
      if (a > b) return a;
      return b;
  }
  
  typedef struct{
      int data;
      int height; // 높이를 저장해야 시간 복잡도를 보장할 수 있음
      struct Node* leftChild;
      struct Node* rightChild;
  } Node;
  ```

- AVL 트리의 높이 계산 함수

  ```c
  int getHeight(Node* node){
      if(node == NULL) return 0;
      return node->height;
  }
  
  // 모든 노드는 회전을 수행한 이후에 높이를 다시 계산
  void setHeight(Node* node){
      node->height = getMax(getHeight(node->leftChild), getHeight(node->rightChild)) + 1;
  }
  
  int getDifference(Node* node){
      if(node == NULL) return 0;
      Node* leftChild = node->leftChild;
      Node* rightChild = node->rightChild;
      return getHeight(leftChild) - getHeight(rightChild);
  }
  
  ```

- AVL 트리의 LL 회전

  1. 불균형 발생
     - 빨간색 영역에 새로운 노드가 삽입되는 경우 노드 X를 기준으로 했을 때 불균형이 발생했다는 것을 알 수 있다.
  2. LL 회전
     - 노드 X를 기준으로 LL 회전을 수행하여 트리의 불균형을 해소합니다. 

  ```c
  Node* rotateLL(Node* node){
      Node *leftChild = node->leftChild;
      node->leftChild = leftChild->rightChild;
      leftChild->rightChild = node;
      setHeight(node); // 회전 이후에 높이를 다시 계산
      return leftChild; // leftChild는 이후에 setHeight() 수행
  }
  ```

- AVL 트리의 RR 회전 (LL회전을 반대로 수행)

  ```c
  Node* rotateRR(Node* node){
      Node *rightChild = node->rightChild;
      node->rightChild = rightChild->leftChild;
      rightChild->leftChild = node;
      setHeight(node);
      return rightChild;
  }
  ```

- AVL 트리의 LR 회전

  1. 불균형 발생
     - 빨간색 영역에 새로운 노드가 삽입되는 경우 노드 X를 기준으로 했을 때 불균형이 발생했다는 것을 알 수 있다.
  2. RR 회전
     - 가장 먼저 자신의 왼쪽 노드인 L 노드를 기준으로 RR 회전을 수행하여, 불균형 노드를 왼쪽으로 몰아 넣는다.
  3. LL 회전
     - 이후에 노드 X를 기준으로 LL 회전을 수행하면 불균형이 해소된다.

  ```c
  Node *rotateLR(Node* node){
      Node *leftChild = node->leftChild;
      node->leftChild = rotateRR(leftChild);
      setHeight(node->leftChild); // 회전 이후에 높이를 다시 계산
      return rotateLL(node); //해당 노드는 이후에 setHeight() 수행
  }
  ```

- AVL 트리의 RL 회전(LR 회전을 반대로 수행)

  ```c
  Node *rotateRL(Node* node){
      Node *rightChild = node->rightChild;
      node->rightChild = rotateLL(rightChild);
      setHeight(node->rightChild); // 회전 이후에 높이를 다시 계산
      return rotateRR(node); // 해당 노드는 이후에 setHeight() 수행
  }
  ```

- AVL 트리의 균형 잡기

  - AVL 트리의 균형 잡기는 각 노드가 '삽입 될 때'마다 수행되어야 한다. '삽입' 과정에 소요되는 시간 복잡도는 O(logN)이다. 따라서 각 트리의 균형 잡기는 삽입 시에 거치는 모든 노드에 대하여 수행된다는 점에서 O(1)의 시간 복잡도를 만족해야 한다.

  ```c
  Node* balance(Node* node){
      int difference = getDifference(node);
      if (difference >= 2){
          if (getDifference(node->leftChild) >= 1){
              node = rotateLL(node);
          }
          else{
              node = rotateLR(node);
          }
      }
      else if (difference <= -2){
          if (getDifference(node->rightChild) <= -1){
              node = rotateRR(node);
          }
          else{
              node = rotateRL(node);
          }
      }
      setHeight(node); // 회전 이후에 높이를 다시 계산 - 항상 해줘야함
      return node;
  }
  ```

- AVL 트리의 삽입

  - AVL 트리의 삽입 과정은 일반적인 이진 탐색 트리와 흡사하다. 다만 삽입 시에 거치는 모든 노드에 대하여 균형 잡기를 수행해주어야 한다는 특징이 있다.

  ```c
  Node *insertNode(Node* node, int data){
      if(!node){
          node = (Node*)malloc(sizeof(Node));
          node->data = data;
          node->height = 1;
          node->leftChild = node->rightChild = NULL;
      }
      else if (data < data->data){
          node->leftChild = insertNode(node->leftChild, data);
          node = balance(node);
      }
      else if(data > node->data){
          node->rightchild = insertNode(node->rightChild, data);
          node = balance(node);
      }
      else{
          printf("데이터 중복이 발생했습니다. \n");
      }
      return node;
  }
  ```

- AVL 트리의 출력 함수

  - AVL 트리는 삽입되는 과정을 면밀히 살펴보는 것이 중요하므로, 트리 구조를 적절히 보여 줄 수 있는 방식으로 출력해야 합니다. 일반적으로 트리의 너비가 높이보다 크다는 점에서 세로 방향으로 출력하는 함수를 구현할 수 있습니다.

  ```c
  Node* root = NULL;
  void display(Node* node, int level){
      if(node != NULL){
          display(node->rightChild, level + 1);
          printf("\n");
          if(node == root){
              printf("Root: ");
          }
          for(int i = 0; i < level && node != root; i++){
              printf("    ");
          }
          printf("%d(%d)", node->data, getHeight(node));
          display(node->leftChild, level + 1);
      }
  }
  ```

- AVL 트리 이용해보기

  ```c
  int main(void){
      root = insertNode(root, 7);
      root = insertNode(root, 6);
      root = insertNode(root, 5);
      root = insertNode(root, 3);
      root = insertNode(root, 1);
      root = insertNode(root, 9);
      root = insertNode(root, 8);
      root = insertNode(root, 12);
      root = insertNode(root, 16);
      root = insertNode(root, 18);
      root = insertNode(root, 23);
      root = insertNode(root, 21);
      root = insertNode(root, 14);
      root = insertNode(root, 15);
      root = insertNode(root, 19);
      root = insertNode(root, 20);
      display(root, 1);
      printf("\n");
      system("pause");
  }
  ```

- 요약
  - 편향 이진 트리(Skewed Binary Tree)의 경우 탐색에 있어 O(N)의 시간 복잡도를 가진다.
  - 따라서 AVL 트리를 이용하여 탐색에 있어서 O(logN)의 시간 복잡도를 유지할 수 있다.
  - 상당히 고급 자료구조. 자유자재로 다룬다면 포인터의 개념과 자료구조의 개념을 바르게 잡았다는 것. 

> 2019-04-28

### 38강 - 해시

- 해시(Hash)는 데이터를 최대한 빠른 속도로 관리하도록 도와주는 자료 구조

- 해시를 사용하면 메모리 공간이 많이 소모되지만 매우 빠른 속도로 데이터를 처리할 수 있다.

- 빠르게 데이터에 접근할 수 있다는 점에서 데이터베이스 등의 소프트웨어에서 활용

- 특정한 값(Value)을 찾고자 할 때는 그 값의 키(Key)로 접근할 수 있다. 일반적으로 해시 함수는 모듈로(Modulo) 연산 등의 수학적 연산으로 이루어져 있으므로 O(1)만에 값에 접근할 수 있다.

- 해시의 충돌

  - 해시 함수의 입력 값으로는 어떠한 값이나 모두 들어갈 수 있지만, 해시 함수를 거쳐 생성되는 키(Key)의 경우의 수는 한정적이기 때문에 키(Key) 중복이 발생할 수 있다.
  - 해시 테이블에서 키(Key)가 중복되는 경우 충돌(Collision)이 발생했다고 표현

- 생일의 역설

  - 무작위의 사람 57명을 한 곳에 모아 놓으면, 2명의 생일이 같을 확률이 99%이다.
  - 이를 해싱(Hashing) 과정과 비교하자면 '365로 나눈 나머지'를 키로 이용하는 해시 함수의 경우 입력 데이터가 57개만 되어도 사실상 충돌이 무조건 발생한다고 판단해야 하는 것

- 해싱(Hashing)

  - 해싱 알고리즘은 나눗셈 법(Division Method)이 가장 많이 활용된다. 입력 값을 테이블의 크기로 나눈 나머지를 키(Key)로 이용하는 방식. 테이블의 크기는 소수(Prime Number)로 설정하는 것이 효율성이 높다.

- 충돌을 처리하는 방법

  - 아무리 잘 만들어진 해시 함수라고 해도 충돌이 발생할 수 밖에 없다. 충돌을 처리하는 방법은 다음과 같이 두 가지 유형으로 분류

    1. 충돌을 발생시키는 항목을 해시 테이블의 다른 위치에 저장 : 선형 조사법, 이차 조사법 등
    2. 해시 테이블의 하나의 버킷(Bucket)에 여러 개의 항목을 저장 : 체이닝(Chaining) 등

  - 선형 조사법 : 충돌하면 그 다음 자리에 넣는다.

    - 선형 조사법 구조체 정의

      ```c
      #define _CRT_SECURE_NO_WARNINGS
      #include <stdio.h>
      #include <stdlib.h>
      #include <string.h>
      #include <time.h>
      #define TABLE_SIZE 10007
      #define INPUT_SIZE 5000
      
      typedef struct{
          int id;
          char name[20];
      } Student;
      ```

    - 선형 조사법 해시 테이블의 초기화 및 반환 함수

      ```c
      // 해시 테이블을 초기화합니다.
      void init(Student** hashTable){
          for(int i = 0; i < TABLE_SIZE; i++){
              hashTable[i] = NULL;
          }
      }
      
      // 해시 테이블의 메모리를 반환합니다.
      void destructor(Student** hashTable){
          for(int i = 0; i < TABLE_SIZE; i++){
              if(hashTable[i] != NULL){
                  free(hashTable[i]);
              }
          }
      }
      ```

    - 선형 조사법 데이터 탐색 함수

      ```c
      // 해시 테이블 내 빈 공간을 선형 탐색으로 찾는다.
      int findEmpty(Student** hashTable, int id){
          int i = id % TABLE_SIZE;
          while(1){
              if(hashTable[i % TABLE_SIZE] == NULL){
                  return i % TABLE_SIZE;
              }
              i++;
          }
      }
      
      // 특정한 ID 값에 매칭되는 데이터를 해시 테이블 내에서 찾는다.
      int search(Student** hashTable, int id){
          int i = id % TABLE_SIZE;
          while(1){
              if(hashTable[i % TABLE_SIZE] == NULL) return -1;
              else if (hashTable[i % TABLE_SIZE]->id == id) return i;
              i++;
          }
      }
      ```

    - 선형 조사법 데이터 삽입 및 추출 함수

      ```c
      // 특정한 키 인덱스에 데이터를 삽입한다.
      void add(Student** hashTable, Student* input, int key){
          hashTable[key] = input;
      }
      
      // 해시 테이블에서 특정한 키의 데이터를 반환한다.
      Student* getValue(Student** hashTable, int key){
          return hashTable[key];
      }
      ```

    - 선형 조사법 데이터 출력 함수

      ```c
      // 해시 테이블에 존재하는 모든 테이터를 출력한다.
      void show(Student** hashTable){
          for (int i = 0; i < TABLE_SIZE; i++){
              if (hashTable[i] != NULL){
                  printf("키 : [%d] 이름 : [%s]\n", i, hashTable[i]->name);
              }
          }
      }
      ```

    - 선형 조사법 해시 테이블 사용

      ```c
      int main(void){
      	Student **hashTable;
          hashTable = (Student**)malloc(sizeof(Student) * TABLE_SIZE);
          init(hashTable);
          
          for (int i = 0; i < INPUT_SIZE; i++){
              Student* student = (Student*)malloc(sizeof(Student));
              student->id = rand() % 1000000;
              sprintf(student->name, "사람%d", student->id);
              if(search(hashTable, student->id) == -1){
                  // 중복되는 ID는 존재하지 않도록 함
                  int index = findEmpty(hashTable, student->id);
                  add(hashTable, student, index);
              }
          }
          
          show(hashTable);
          destructor(hashTable);
          system("pause");
          return 0;
      }
      ```

    - 선형 조사법의 단점

      - 선형 조사법은 충돌이 발생하기 시작하면, 유사한 값을 가지는 데이터끼리 서로 밀집되는 **집중 결합** 문제가 존재
      - 물론 선형 조사법이라고 해도 '해시 테이블의 크기'가 비약적으로 크다면, 다시 말해 메모리를 많이 소모한다면 충돌이 적게 발생하므로 매우 빠른 데이터 접근 속도를 가질 수 있음
      - 하지만 일반적인 경우, 해시 테이블의 크기는 한정적이므로 충돌이 최대한 적게 발생하도록 해야 함.

  - 이차 조사법

    - 이차 조사법은 선형 조사법을 약간 변형한 형태로 키 값을 선택할 때 '완전 제곱수'를 더해 나가는 방식

  - 조사법의 테이블 크기 재설정

    - 일반적으로 선형 조사법, 이차 조사법 등의 조사법에서 테이블이 가득 차게 되면 테이블의 크기를 확장하여 계속해서 해시 테이블을 유지할 수 있도록 한다.

  - 체이닝

    - 체이닝(Chaining) 기법은 연결 리스트를 활용해 특정한 키를 가지는 항목들을 연결하여 저장한다.

    - 연결 리스트를 사용한다는 점에서 삽입과 삭제가 용이. 또한 테이블 크기 재설정 문제는 '동적 할당'을 통해서 손쉽게 해결 할 수 있다. 다만 동적 할당을 위한 추가적인 메모리 공간이 소모된다는 단점이 있다.

    - 체이닝 구조체 정의

      ```c
      #define _CRT_SECURE_NO_WARNINGS
      #include <stdio.h>
      #include <stdlib.h>
      #include <string.h>
      #include <time.h>
      #define TABLE_SIZE 10007
      #define INPUT_SIZE 5000
      
      typedef struct{
          int id;
          char name[20];
      } Student;
      
      typedef struct{
          Student* data;
          struct Bucket* next;
      } Bucket;
      ```

    - 체이닝 해시 테이블의 초기화 및 반환

      ```c
      // 해시 테이블을 초기화한다
      void init(Bucket** hashTable){
          for(int i = 0; i < TABLE_SIZE; i++){
              hashTable[i] = NULL;
          }
      }
      
      // 해시 테이블의 메모리를 반환한다.
      void destructor(Bucket** hashTable){
          for (int i = 0; i < TABLE_SIZE; i++){
              if (hashTable[i] != NULL){
                  free(hashTable[i]);
              }
          }
      }
      ```

    - 체이닝 데이터 탐색 함수

      ```c
      int isExist(Bucket** hashTable, int id){
          int i = id & TABLE_SIZE;
          if (hashTable[i] == NULL) return 0;
          else{
              Bucket *cur = hashTable[i];
              while (cur != NULL){
                  if (cur->data->id == id) return 1;
                  cur = cur->next;
              }
          }
          return 0;
      }
      ```

    - 체이닝 데이터 삽입 함수

      ```c
      // 특정한 키 인덱스에 데이터를 삽입한다.
      void add(Bucket** hashTable, Student* input){
          int i = input->id % TABLE_SIZE;
          if (hashTable[i] == NULL){
              hashTable[i] = (Bucket*)malloc(sizeof(Bucket));
              hashTable[i]->data = input;
              hashTable[i]->next = NULL;
          }
          else{
              Bucket *cur = (Bucket*)malloc(sizeof(Bucket));
              cur->data = input;
              cur->next = hashTable[i];
              hashTable[i] = cur;
          }
      }
      ```

    - 체이닝 데이터 출력 함수

      ```c
      // 해시 테이블에 존재하는 모든 데이터를 출력한다.
      void show(Bucket** hashTable){
          for (int i = 0; i < TABLE_SIZE; i++){
              if(hashTable[i] != NULL){
                  Bucket *cur = hashTable[i];
                  while(cur != NULL){
                      printf("키 : [%d] 이름 : [%s]\n", i, cur->data->name);
                      cur = cur->next;
                  }
              }
          }
      }
      ```

    - 체이닝 해시 테이블 사용해보기

      ```c
      int main(void){
          Bucket **hashTable;
          hashTable = (Bucket**)malloc(sizeof(Bucket) * TABLE_SIZE);
          init(hashTable);
          
          for(int i = 0; i < INPUT_SIZE; i++){
              Student* student = (Student)malloc(sizeof(Student));
              student->id = rand() % 1000000;
              sprintf(student->name, "사람%d", student->id);
              if(!isExist(hashTable, student->id)){
                  // 중복되는 ID는 존재하지 않도록 함.
                  add(hashTable, student);
              }
          }
          
          show(hashTable);
          destructor(hashTable);
          system("pause");
          return 0;
      }
      ```

- 요약

  - 해시(Hash)는 이론적으로 데이터의 삽입과 삭제에 있어서 O(1)의 시간 복잡도를 가진다.
  - 해시는 데이터베이스 인덱싱 및 정보보안 관련 모듈 등에서 굉장히 다양하게 사용되고 있다.

> 2019-05-11

### 39강 - 프림 알고리즘

- 최소 신장 트리

  - **신장 트리란 특정한 그래프에서 모든 정점을 포함하는 그래프**
  - 최소 신장 트리는 스패닝 트리 중에서 **간선의 가중치 합이 가장 작은 트리**를 의미

- 프림 알고리즘

  1. 그래프에서 정점 하나를 선택하여 트리 T에 포함시킨다.
  2. T에 포함된 노드와 T에 포함되지 않은 노드 사이의 간선 중에서 가중치가 가장 작은 간선을 찾는다.
  3. 해당 간선에 연결된 T에 포함되지 않은 노드를 트리 T에 포함시킨다.
  4. 모든 노드가 포함될 때까지 2와 3을 반복한다.

  - 프림 알고리즘은 각 간선에 대한 정보를 우선순휘 큐에 담아 처리하는 방식으로 구현할 수 있다.

- 3분 30초부터 - 프림 알고리즘 간선 구조체 정의 부터







- **자료구조 책 보고 내용 추가 및 보충심화 할 것 ** 











<!--stackedit_data:
eyJoaXN0b3J5IjpbNDgwMTgzOTcyXX0=
-->
