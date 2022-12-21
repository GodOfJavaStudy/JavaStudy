### 4장) 정보를 어디에 넣고 싶은데?

## 1. 변수란?
 - 내용을 담는 것 
 - 항상 이름이 정해져야 함.

## 2. 자바의 4가지 변수
 - 지역변수 : 중괄호 내에서 선언된 변수
 - 매개변수 : 메소드에 넘겨주는 변수
 - 인스턴스 변수 : 클래스 안,메소드 밖에 선언된 변수 (static 예약어 존재 x)
 - 클래스 변수 :  클래스 안,메소드 밖에 선언된 변수 (static 예약어 존재o)

## 3. 변수 유효 시점
 - 지역변수 -> 중괄호 내에서만 유효
 - 매개변수 -> 메소드 호출 시 생성, 메소드 종료 시 소멸
 - 인스턴스 변수 -> 객체 생성 시 생성,객체를 참조하고 있는 객체가 없을 시 소멸
 - 클래스 변수 -> 클래스 최초 호출 시 생성 , 자바 프로그램 종료 시 소멸

```
    int instVariable;                  // 인스턴스변수 (static x)
    static int classVariable;         // 클래스변수    (static o)
    
    public void method (int param) { // 매개변수
        int localVariable;          // 지역변수
    }
```
## 4. 변수 이름은 이렇게!
 - 길이제한x
 - 첫번째 문자 (유니코드,알파벳,$,_)만 가능함.
 - 두번째 문자 (유니코드,알파벳,숫자,$,_) 모두 사용가능함.
 - camel case 적용 .. ex) testNum
 - 상수는 모두 대문자,단어사이에는 '_'로 구분 .. 상수는 절대 변하지 않는 값

## 5. 자바의 두 가지 자료형
 - 기본형 -- ex) int a = 10;
 - 참조형 : new 예약어를 사용하여 초기화 하는 자료형 --
 ex) String str = new String("test");

## 6. 기본 자료형 8가지
 - 정수형 : byte, short, int, long, char
 - 소수형 : float,double
 - 기타형 : boolean


