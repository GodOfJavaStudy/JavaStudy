# 1장 프로그래밍이란 무엇인가
*********************************

* 프로그래밍이란  
  * 사람과 컴퓨터 사이의 언어
  * java, c, c++, python 등등
  
-------------------

```
public boolean checkPassword(String password){

}
```
* public : 접근제어자
* boolean : 리턴타입
* checkPassword : 메소드 이름
* (String password) : 매개 변수  
--> 접근제어자 리턴타입 메소드이름 (매개변수) 이 순으로 써야된다 안그러면 에러를 뱉어낸다  

-----------------------------

## Class
* 자바의 가장 작은 단위는 클래스다
* method(메소드)는 어딘가 소속이 되어야 되는데 그 소속은 class이다  
```java
public class DoorLockManager {

}
```
* 클래스 선언은 접근제어자 class 클래스이름 으로 작성해야 된다

```java
public class DoorLockManger{
    public boolean checkPassword(String password){
        // 생략
    }

  public void setPassword(String password){
    // 생략
  }

  public void resetPassword(){
    // 생략
  }
}
```
* // 주석(comment)이며 어떤 줄을 실행하지 않도록 할 때 사용한다
* checkPassword(password) 의 boolean 이라는 리턴타입이 정의 되어 있는데 이것은 기본 자료형 중 하나다
* setPassword(password) 의  리턴타입의 void는 메소드를 돌려줄게 없다라고 이야기 해주는 것이다 즉 아무런 값을 돌려주지 않는다
* resetPassword() 들어가는 값도 없고 돌려주는 값도 없다 

### 클래스는 상태를 갖고 있어야 된다
* 자바와 같은 언어를 객제치향 프로그래밍 언어(Object Oriented Programming Language)라고 한다
* 객체지향 언어는 현실 세계를 프로그램으로 표현할 수 있다
* 사물이 클래스도 될 수 있지만 추상적인 것도 클래스가 될 수 있다  
  * 사물(도어락) 추상적(쇼핑몰 장바구니)
* 클래스의 조건은 상태(state)와 행동(behavior)이 있어야만 한다
  * 행동 : 메소드
  * 상태 : 클래스의 속성을 결정 짓는 것
    * 상태는 클래스 안에 , 메소드 밖에 정의 한다

```java
public class DoorLockManger {
    
    String currentPassword;
    
    public boolean checkPassword(){
        // 생략
    }
    // 이하 생략
}
```
* 어떤 값을 포함 할 currentPassword와 같은 것을 변수(variable)이라고 한다. 이 변수는 클래스의 특성을 결정짓는 "상태"에 속한다
* !! 꼭 상태와 행동이 있어야 되는 것은 아니다

## * 프로그램의 가장 기본은 =를 이해하는 것
* 프로그램에서는 왼쪽에 대입을 할 변수를 오른쪽에는 계산식을 적어야 한다
```java
int a; //a라는 변수를 선언 
a = 1+2; // a에 1+2의 값을 대입(할당)한다
```
* 변수 선언이란 값을 할당하지 않은 것 ex) int a; String b;
* 변수를 선언할 때는 타입 변수명; 으로 한다 ex) int a; String b;
* 변수 초기화란 변수 선언 후 처음으로 값을 대입하는 것 ex) int a = 3; String b = "black"; 
  * int a = 3; 변수 선언과 초기화를 같이 한것 
  * 변수는 하나의 값만 저장 한다 int a = 3; a = 4; 면 기존의 값이 지워지고 새로운 값 4가 저장된다
```java
public class Calculator {
    
    public int add(int num,int num2){
        int sum;
        sum = num + num2;
        return sum; // sum을 리턴한다
    }
    // 이하 생략
}
```
* add() 라는 메소드의 가장 마지막 줄의 return은 어떤 값을 돌려줄 때 지정해야 된다

| 연산 종류 | 기호  | ex (10, 5)  | 결과  |
|:-----:|:---:|:-----------:|:---:|
|  더하기  |  +  | num1 + num2 | 15  |
|  빼기   |  -  | num1 - num2 |  5  |
|  곱하기  |  *  | num1 * num2 | 50  |
|  나누기  |  /  | num1 / num2 |  1  |

--------------

## 한줄을 의미하는 세미콜론
```java
public class Calculator {
    
    public int add(int num,int num2){
        int sum;
        sum = num + num2;
        
        sum =
                num +
                        num2; // 세미콜론 기준으로 한줄 
        return sum; 
    }
    // 이하 생략
}
```
* 세미콜론(;)은 모든 자바 코드의 한 줄이 끝날 때 적어 주는 것
* 자바에서는 컴파일이 세미콜론이 나올 때 까지 한 줄 이라고 생각한다


* 인덴트(indent)란 코드 앞의 공백을 얘기한다
```java
public class Calculator { 
    public int add(int num,int num2){ // 탭 한번
        int sum; // 탭 두번
        sum = num + num2;
        return sum; 
    } // 탭한번
}
```

## 모든 프로그래밍 언어에는 예약어 라는 것이 있다
* 예약어 : 예약되어 있으니깐 다른 용도로 쓰지 못하는 단어
* 클래스이름, 메소드이름, 변수이름, 등으로 쓸 수 없다
  * int int; 이렇게 쓸 수 없다
  * 