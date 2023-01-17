# 20장 
## 가장 많이 쓰는 패키지는 자바랭
### java.lang 패키지는 특별하죠
- 이 절의 제목처럼 java.lang 패키지 아주 특별한 패키지다.
    - 자바의 패키지 중에서 유일하게 java.lang. 패키지에 있는 클래스들은 import를 안해도 사용할 수 있기 때문이다.
- java.lang 과 java.util 패키지를 제외한 대부분의 java로 시작하는 패키지들은 패키지 이름만 보고도 어떤일을 할 때 사용하는지를 알 수 있다.
- java.lang 패키지에서 제공하는 인터페이스, 클래스 , 예외 클래스 등은 다음과 같이 분류할 수 있다.

    - 언어 관련 기본
    - 문자열 관련
    - 기본 자료형 및 숫자 관련
    - 쓰레드 관련
    - 예외 관련
    - 런타임 관련
- java.lang 패키지에 정의되어 있는 "에러"는 다음과 같다.
  - AbstractMethodError, AssertionError, ClassCircularityError, ClassFormatError, Error, 
    ExceptionInInitializerError, IllegalAccessError, IncompatibleClassChangeError,
    InstantiationError, InternalError, LinkageError, noCLassDefFoundError, NoSuchFieldError,
    NoSuchMethodError, OutOfMemoryError, StackOverFlowError, ThreadDeath, UnknownError,
    UnsatisfiedLinkError, UnsupportedClassVersionError, VerifyError, VirtualMachineError
    
- java.lang 패키지에는 앞서 살펴본 자바의기본 어노테이션이 선언되어 있다.
    - Deprecated
    - Override
    - Suppress Warnings
    
### 숫자를 처리하는 클래스들 
- 간단한 계산을 할 때에는 대부분 기본 자료형 Primitive Type을 사용한다.
- 기본 자료형은 자바의 힙Heap 이라는 영역에 저장되지 않고, 스택이라는 영역에 저장되어 관리된다. (처리가 빠름)
- 숫자를 객체로 처리해햘 필요가 있는 경우
    - Byte(byte)
    - Short (short)
    - Integer (int)
    - Long (long)
    - Float (float)
    - Double (double)
    - Character
    - Boolean
    
- 위는 Wrapper클래스라고 불리며 , 모두 Number 라는 abstract 클래스를 확장(extends)한다.
- 기본 자료형처럼 사용이 가능하다. ( 자바 컴파일러에서 자동으로 형 변환을 해주기 때문이다.)
- Character 클래스를 제외하고는 공통적인 메서드를 제공한다. 
- 바로 Parse 타입이름() 메서드와 valueOf()라는 메서드다. 
    - parse 타입 이름() 메서드는 기본 자료형을 리턴
    - valueOf() 메서드는 참조 자료형을 리턴한다.
    
- 매개 변수를 참조 자료형으로만 받는 메서드를 처리하기 위해서
- 제네릭과 같이 기본 자료형을 사용하지 않는 기능을 사용하기 위해서 (제네릭에 대해서는 다음 장에서 알아본다.)
- MIN_VALUE(최소값)나 MAX_VALUE(최대값)와 같이 클래스에 선언된 상수 값을 사용하기 위해서
- 문자열을 숫자로, 숫자를 문자열로 쉽게 변환하고, 2,8.10.16진수 변환을 쉽게 처리하기 위해서 
  
- Boolean 클래스를 제외하고 모두 MIN_VALUE 와 MAX_VALUE라는 상수를 갖고 있다.
  - Character의 경우는 그냥 출력할 경우 `char`타입으로 출력되므로 알아보기 힘들기 떄문에 `int`타입으로 변환하여 그 값을 확인하도록 해놓았다.
  - `Integer` 타입과 `Long`타입을 읽기가 어렵다.
  - 이 값을 2 진수나 16진수로 표현하면 조금은 더 편한다.
    - `Integer` 최소값과 최대값을 2진수와 16진수로 나타낸 결과를 보려면, `Integer`클래스에서 제공하는 `toBinaryString()`이라는 메서드를 사용하면 된다
```java
package c;

class NumT{
    public void integerMinMaxCheckBinary(){
        System.out.println("Integer BINARY min= " + Integer.toBinaryString(Integer,MIN_VALUE));
        System.out.println("Integer BINARY min= " + Integer.toBinaryString(Integer,MAX_VALUE));
        
        
        System.out.println("Integer HEX min= " + Integer.toHexString(Integer,MAX_VALUE));
        System.out.println("Integer BINARY min= " + Integer.toHexString(Integer,MAX_VALUE));
    }
}

```
- 돈 계산등을 수행할 때 정수형은 BigInteger, 소수형은 BigDecimal을 사용하여야 정확한 계산이 가능하다.
- 이 두 클래스들은 모두 java.lang.Number 클래스의 상속을 받았으며 java.math 패키지에 선언되어 있다.

### 각종 정보를 확인하기 위한 System 클래스
- 생성자가 없다.
  - System 클래스의 3개의 static 변수가 선언되어 있다.

|선언 및 리턴 타입|변수명|설명|
|-------|-----|-----|----|
|static PrintStream| err | 에러 및 오류를 출력할 때 사용한다.|
|static InputStream|in | 입력값을 처리할 때 사용한다.|
|static PrintStream|out| 출력값을 처리할 때 사용한다.|

- 출력과 관련된 메서드는 System 클래스에서 찾으면 안돠고 PrintStream 클래스에서 찾아야한다. 
  - PrintStream과 InputStream은 모두 `java.io`패키지에 선언되어 있다.
- `System` 클래스는 이름 그 대로 시스템에 대한 정보를 확인하는 클래스이다.
  - 시스템 속성(Property)값 관리
  - 시스템 환경 (Environment)값 조회
  - GC 수행
  - JVM 종료
  - 현재 시간 조회
  - 기타 관리용 메서드

#### 시스템 속성 관리

|리턴 타입|메서드 이름 및 매개변수|설명|
|-------|-------------------|---|
|static String| clearProperty(String key)|key에 지정된 시스템 속성을 제거한다.|
|static Properties|getProperties()|현재 시스템 속성을 `Properties` 클래스 형태로 제공한다.|
|static String|getProperty(String key) |key에 지정된 문자열로 된 시스템 속성값(value)를 얻는다.|
|static String|getProperty(String key,String def)|key에 지정된 문자열로된 시스템 속성(value)를 얻고, 없으면 def에 지정된 값을 리턴|
|static void | setProperties(Properties props)|Properties 타읍으로 넘겨주는 매개 변수에 있는 값들을 시스템 속성에 넣는다.|
|Static String|setProperty(String key,String value)|key에 지정된 시스템 속성의 값을 value로 대체한다.|

#### Property를 이해하려면 `Properties`라는 클래스를 알아야 한다.
- `Properties`는 `java.util` 패키지에 속하며, `Hashtable`의 상속을 받은 클래스다.
- 컬렉션(Collection)관련 클래스들에 대해서 배우면 `Hashtable`이 어떤 클래스인지 알 수 있다.

#### 시스템 환경(Environment) 값 조회
|리턴 타입|메서드 이름 및 매개 변수|설명|
|-------|--------------------|---|
|static Map<String, String>|getenv()|현재 시스템 환경에 대한 Map 형태의 리턴 값을 받는다.|
|static String|getenv(String name)|지정한 name에 해당하는 값을 받는다.|

#### GC 수행
|리턴 타입|메서드 이름 및 매개 변수|설명|
|-------|--------------------|---|
|static void| gc()|가비지 컬렉터를 실행한다.|
|static void|runFinalization()|GC처리를 기다리는 모든 객체에 대하여 `finalize()` 메서드를 실행한다.|

#### JVM 종료
|리턴 타입|메서드 이름 및 매개 변수|설명|
|-------|--------------------|---|
|static void|exit(int status)|현재 수행중인 JVM을 멈춘다.|

#### 현재 시간 조회
|리턴 타입|메서드 이름 및 매개 변수|설명|
|-------|--------------------|---|
|static long|currentTimeMillis()|현재 시간을 밀리초 단위로 리턴.|
|static long | nanoTime() | 현재 시간을 나노초 단위로 리턴한다.|

> 밀리초는 1/1,000초 , 나노초는 1/1,000,000,000 초.

### System.out을 살펴보자
- System클래스에 선언되어 있는 out(System.out)과 err(System.err) 변수는 PrintStream이라는 동일한 클래스의 객체다.  
  - print()
  - println()
  - format()
  - printf()
  - write()

`println("");` 로 처리하면 String 객체가 생기므로 `println();`으로 처리하는 것이 깔끔하다.

