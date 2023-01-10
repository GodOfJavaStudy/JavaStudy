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
  
  
- 돈 계산등을 수행할 때 정수형은 BigInteger, 소수형은 BigDecimal을 사용하여야 정확한 계산이 가능하다.
- 이 두 클래스들은 모두 java.lang.Number 클래스의 상속을 받았으며 java.math 패키지에 선언되어 있다.
