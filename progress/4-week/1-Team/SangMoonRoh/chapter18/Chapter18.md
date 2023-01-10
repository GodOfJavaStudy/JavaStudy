# 18장
## 이제 기본 문법은 거의 다 배웠으니 정리해 봅시다.
### 객체지향 개발과 관련된 용어들
- 클래스(Class)
- 상태(state)와 행위(behavior)
- 캡슐화(Encapsulation)
- 메시지(Message)
- 객체(Object)
- 상속(Inheritance
- Overriding
- 다형성(Polymorphism)
- Overloading

### 클래스(Class)
- "상태"와 "행위"를 갖는 자바의 기본 단위를 의미한다.

### 상태(state)와 행위(behavior)
- 어떤 사물을 나타낼 때에는 상태와 행위로 구분하여 표시하는 것이 가능하다. 자바에서 "상태"는 클래스나 인스턴스 변수로,  
  "행위"는 메소드로 표현할 수 있다.
  
```java
package c;
public class Common {
  private int state; // 상태
  public void setState(int newState) { // 행위
  }
}
```

### 캡슐화 (Encapsulation)
- 연관된 "상태"와 "행위"를 결정하는 기능을 묶어 주는 것을 의미한다. 이렇게 묶어 주면 기능을 클래스 밖에서 접근 가능한 대상을 제한하는 정보 은닉(information hiding)이 가능하다.  
그리고, 하나의 객체를 위한 코드가, 다른 객체를 위한 코드와 무관하게 수행할 수 있는 모듈화(modularity)가 가능해진다. 이처럼 묶여 있는 가장 작은 단위를 클래스라고 본다.
```java
public class Common {
    private int state; //private 로 선언함으로써 정보 은닉
    public void setState(int newState){ //상태를 변경 가능
    }
}
```

### 메시지(Message)
- 메서드에서 다른 메서드를 호출할 때 전달하는 값을 메시지라고 한다.  
자바에서는 여러분들이 메서드를 호출할 때 넘겨주는 매개 변수들이 여기에 속한다.  
위의 코드에서 newState가 메시지를 의미하는 매개 변수이다.
  
### 객체(Object)
- 클래스는 사물의 단위를 의미하지만, 객체는 각 사물을 의미한다.  
예를 들면 `godOfJava`는 책 중의 하나를 의미하는 객체라고 볼 수 있다.
```java
Book godOfJava = new Book();
```
지금까지 살펴본 클래스의 main() 메서드에서 가장 첫 줄에서 생성한 것들이 바로 이 객체다.

### 상속
- 부모에 선언된 변수와 메서드에 대한 사용권을 갖는 것을 말한다.  
즉, 클래스 선언시 extends를 사용하여 확장하거나, implements를 사용하여 구현한 경우가 여기에 속한다.
  
### 다형성
- 이 세상에 부모와 자식이 똑같을 수가 없고, 자식들도 같을 수가 없다. 마찬가지로 자바에서는 부모 클래스에서 파생된 자식 클래스들의 기능이 각기 다를 수 있다는 것을 의미한다.
```java
public class Parent {
    public void method() {
    }
}
```
이러한 부모 클래스가 있을 때
```java
public class FirstChild extends Parent { // Parent 클래스를 상속 받음
    public void method(){
    }
}
```
와
```java
public class SecondChild extends Parent { // Parent 클래스를 상속 받음
    public void method(){
    }
}
```
가 `FirstChild`와 `SecondChild`에 있는 `method()`는 다른 기능을 수행해도 무관하다는 것이 다형성이다.

### Overriding
- 부모 클래스에 선언되어 있는 메서드와 동일한 선언을 갖지만 구현이 다른 것을 의미한다.  
자바에서 다형성을 제공하는 하나의 방법이 바로 `Overriding`이다. 예제로 살펴보면.
```java
public class Parent {
    public void method(){
        //내용생략
    }
}
```
이러한 부모가 있을 때
```java
public class Child extends Parent {
    public void method(){
        //내용 생략
    }
}
```
- method ()는 부모 클래스의 method()를 덮어 쓴 Overriding 처리가 된 것이다.

### Overloading
- 메서드의 이름은 동일해도, 매개 변수들을 다르게 하는 것을 의미한다.
그래서, 동일한 기능은 하지만, 메서드에 넘겨줄 수 있는 매개 변수의 타입을 다양하게 함으로써 메서드를 사용하는 다른 개발자가 쉽게 구현할 수 있게 해준다.
```java
public class Overloading{
    public void getData(){
    }
    public void getData(int value){
    }
    public void getData(String value){
    }
}
```

### 자바의 주석문 (Comment)

#### 한 줄 주석 : 일반적으로 해당 줄을 실행하지 않도록 할 때 사용
```java
// 주석 처리 하는 내용
```

#### 블록 주석 : 여러 줄을 실행 하지 않도록 할 때 사용
```java
/* 주석시작
   여기에 있는 문장들은 모두 무시되어 버림
 주석 끝 */
```

#### javadoc을 위한 주석 : API 문서에 설명을 표시할 목적으로 사용
```java
/** 주석시작
 * 여기에는 해당 클래스나 메서드의 설명이 있어야 함
 * 주석 끝 */
```

### 패키지와 import
- 패키지 선언시 유의사항
  - 패키지는 package로 시작하며 하위 패키지로 내려갈 때마다 .을 찍어 주어야 한다.
  - 반드시 소스의 가장 첫 줄에 존재해야 한다.
  - 패키지 이름에 자바 예약어가 포함되면 안 된다.
  - 모두 소문자로 구성하는 것이 일반적이다.
  - 일반적인 패키지는 java나 javax로 시작하면 안 된다.
  - 패키지에 해당하는 폴더에 클래스가 존재하는 것이 일반적이다.
  
- 패키지 선언 예
```java
package com.roadbook.godofjava;
```
- import는
  - 다른 패키지에 있는 클래스를 사용하기 위한 문장이다.
  - 다른 클래스에 static으로 선언되어 있는 접근 가능한 변수를 참조하려면 improt static을 사용한다.
  - 하나의 패키지 내에 있는 모든 클래스를 참조하려면 * 을 사용한다.
  
### 자바에서 사용되는 타입의 종류
- 자바의 타입은 크게 기본 자료형과 참조 자료형으로 나뉜다.

### 자바에서 사용되는 타입의 종류
- 자바의 타입은 크게 기본 자료형과 참조 자료형은 나뉜다.
- 8개의 기본 자료형 : 숫자와 boolean(true, false)을 나타내기 위한 자료형을 의미하며, 우리가 마음대로 추가로 만들 수 없다.
  - 정수형 : byte,short, int, long, char
  - 소수형 : float, double
  - 기타 : boolean
  
- 정수형 값의 범위는 다음과 같다.

|타입|최소|최대|비트 수|
|---|---|----|-----|
|byte|-2^7|2^7-1|8|
|short|-2^15|2^15-1|16|
|int|-2^31|2^31-1|32|
|long|-2^63|2^63-1|64|
|char|0|2^16-1|16|

- 기본 자료형의 기본값은 다음과 같다.
  - byte : 0
  - short : 0
  - int :0
  - long :0L
  - float : 0.0f
  - double: 0.0d
  - char : '\u0000'
  - boolean : false
  
#### 참조 자료형과 기본 자료형의 차이
  - 초기화 할 때 : 기본 자료형은 값을 바로 지정하면 되지만 , 참조 자료형은 일반적으로 new와 생성자를 지정하여 객체를 생성한다.
  - 메서드를 호출 할때의 매개 변수 : 기본 자료형 및 참조 자료형 모두 값을 전달하지만, 참조 자료형 안에 있는 변수들은 참조 주소를 전달한다.
  - 특수한 참조 자료형
      - String : String 클래스는 new 를 이용하여 객체를 생성할 필요가 없는 특수한 클래스다.  
        그리고 + 연산까지 가능한 유일한 클래스다.
        
### 변수 종류
- 지역변수 : 지역 변수를 선언한 곳에서부터 생명이 시작되고 지역 변수를 선언한 중괄호가 끝나면 소멸. 
- 매개 변수 : 메서드가 호출될 때 생명이 시작되고 메서드가 끝나면 소멸 (호출한 메서드에서 넘겨준 참조 자료형은 그대로 살아 있음.)
- 인스턴스 변수 : 객체가 생성될 때 생명이 시작되고, 그 객체를 참조하고 있는 다른 객체가 없으면 소멸.
- 클래스 변수 : 객체가 생성될 때 생명이 시작되고, 자바 프로그램이 끝날 때 소멸.

```java
package c;
public class VariableTypes {
    int instanceVariable;
    static int classVariable;
    
    public void method(int parameter){
        int localVariable;
    } 
}
```

### 계산을 쉽게 도와주는 연산자들
- 연산자의 종류
  - 할당 연산자 : =
  - 사칙 연산자 : +, = , *, / , %( 여기서 +와 -는 더하기 빼기)
  - 대입 연산자 : +=, -=, *=, /= ,%=
  - 단항 연산자 : +, -, ++, --(여기서 +와 -는 양수와 음수를 나타내는 연산자임)
  - 비교 연산자 : ==, !=, >, <, >= ,<=
  - 조건적 논리 연산자 : &&, ||
  - 논리 연산자 : !, &, |, ^
  - 삼항연산자 : ? :
  - Bitwise 연산자 : &(AND), |(OR), ^(XOR), ~(NOT)
  - Bit 이동 연산자 : <<, >> ,>>>
  - Bit 대입 연산자 : &=, |=, ^=, <<= ,>>= ,>>>=
  
#### 연산자 연산 우선 순위 
|레벨|연산자|한글 설명|영문 설명|결합방향|
|---|-----|-------|--------|-------|
|1|[]|배열 요소 접근| access array element|좌 ->우|
| |.|객체 변수 접근|access object member| |
| |,|for 루프의 초기화시에만 | comma| |
| |()| 메서드 호출 | invoke a method| |
| |++|x++로 사용할 경우 |post-increment| |
| |--|x--로 사용할 경우 | post-decrement| |
|2|++| ++x로 사용할 경우 | pre-increment|우-> 좌|
| |--| --x로 사용할 경우 | pre-decrement| |
| |+|+x| unary plus | |
| |-|-x| unary minus| | 
| |!| | logical NOT| |
| |~| | bitwise NOT | | 
|3|()| 형 변환시 소괄호 | cast | 우->좌|
| |new | 객체 생성 | object creation | |
|4|* / % | 배수 연산| multiplicative | 좌->우|
|5| +- | 증감 연산 | additive | 좌->우|
| |+ |문자열 더하기 | string concatenation | |
|6| << >> >>>| Bit 이동 연산 | shift | 좌->우|
|7|< <= > >=| 비교 연산 | relational | 좌 -> 우|
| | instanceof| 타입 비교 연산| type comparison | |
|8| == != | 비교 연산| equality | 좌 ->우|
|9| & | 비트 AND | bitwise AND | 좌-> 우|
|10|^ | 비트 XOR | bitwise XOR | 좌-> 우|
|11| \| 비트 OR  | bitwise OR| 좌-> 우|
|12|&&| 조건 논리 AND | conditional AND |좌 -> 우|
|13| \\| 조건 논리 OR | conditional OR |좌 -> 우|
|14| ? : | 삼항 연산 | conditional | 우 -> 좌|
|15| += == *= /= %= &= ^= \= <<= >>= >>>= |할당 연산 | assignment | 우 -> 좌 |

### 조건문들
- if
- if- else
- if- else if
- switch - case

### 반복문들
- while
- do-while
- for 루프
  - break
  - continue
  
### 아무나 사용 못하게 막아주는 접근 제어자
- public
- protected
- (package- private)
- private

### 선언할 때 사용할 수 있는 각종 제어자들

|제어자|클래스|메서드|변수|
|-----|----|-----|---|
|접근 제어자 : public, protected, private| O | O | O |
|구현 필요 제어자 : abstract | O | O | X |
|하나의 인스턴스만 허용하는 제어자 static | O | O | O |
|값 수정 제한 제어자 : final | O | O | O |
|strict 소수 값 제어자  : strictfp | O | O | X |
|어노테이션 | O | O | O |
|동시 접근 제어자 : synchronized | X | O | X |
|다른 언어로 구현된 것을 명시하는 제어자 : native | X | O | X |
|실행시의 동작 방법을 알리는 제어자 : transient, volatile| X | O | O |

- 인터페이스와 abstarct 클래스, 클래스의 차이
  - 인터페이스
    - 어떤 메서드가 존재해야 하는지에 대한 선언만 되어 있다.
    - 절대로 구현되어 잇는 메서드가 있어서는 안된다.
    - 인터페이스를 구현하는 클래스에서는 implements를 사용하여 선언한다.
  - abstract 클래스
    - 구현되어 있는 메서드가 있어도 상관 없다.
    - abstract 으로 선언된 메서드가 1개 이상일 경우에는 반드시 abstract 클래스로 선언해야 한다.
    - abstract 으로 선언된 메서드는 절대로 구현되어 있어서는 안 된다.
    - abstract 클래스를 확장하는 클래스에서는 extends를 사용하여 선언한다.
  
### 자주 사ㅓ용하게 되는 상속
- 생성자
  - 자식 클래스의 생성자가 호출되면 자동으로 부모 클래스의 매개 변수가 없는 기본 생성자가 호출됨. 명시적으로 super() 라고 지정 가능.
  - 부모 클래스의 생성자를 명시적으로 호출하려면 super()를 사용하면 된다.
- 메서드
  - 부모 클래스에 선언된 메서드들이 자신의 클래스에 선언된 것처럼 사용 가능하다. (private 제외)
  - 부모 클래스에 선언된 메서드와 동일한 시그니처를 사용함으로써 메서드 overriding이 가능하다.
  - 부모 클래스에 선언되어 있지 않은 이름의 새로운 메서드 선언이 가능하다.
- 변수
  - 부모 클래스에 private로 선언된 변수를 제외한 모든 변수가 자신의 클래스에 선언된 것처럼 사용 가능
  - 부모 클래스에 선언된 변수와 동일한 이름을 가지는 변수 선언 가능( 권장X)
  - 부모 클래스에 선언되어 있지 않은 이름의 변수 선언 가능
  
### 예외를 처리하자
- try - catch 문

- 예외의 종류 
  - checked excpetion : try- catch로 묶어 줘야 하는 예외, 컴파일시 예외 처리 여부 체크
  - error : 자바 프로세스에 영향을 주는 예외이며, 실행시 발생한다.
  - runtime exception 혹은 unchecked exception : try-catch 로 묶지 않아도 컴파일시 쳌르르 하지 않는 예외이고, 실행시 발생하는 예외.
- throw와 throws
  - throw : 예외 객체를 던지기 위해서 사용.
  - throws : 예외가 발생하면 던질 것이라고 메서드 선언시에 사용한다.
  - 메서드를 선언할 때 매개 변수 소괄호 뒤에 throws라는 예약어를 적어 준 뒤 예외를 선언하면 해당 메서드에서 선언한 예외가 발생하면 호출한 메서드로 예외가 전달.
  - 두 가지 이상의 예외를 던지게 된다면 implement처럼 콤마로 구분하여 예외 클래스 이름을 적어준다.
  - try 블록 내에서 예외를 발생시킬 경우에는 throws라는 예약어를 적어 준 뒤 예외 객체를 생성하거나 생성되어 있는 객체를 명시한다.
  - throw 한 예외 클래스가 catch 블록에 선언되어 있지 않거나, throws 선언에 포함되어 있지 않으면 컴파일 에러가 발생한다.
  - catch 블록에서 예외를 throw 할 경우에는 메서드 선언의 throws 구문에 해당 예외가 정의되어 있어야 한다.
  
  
  
  

  
  
  
  

