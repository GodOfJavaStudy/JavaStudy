## 기본문법
****

### 변수
* 프로그래밍 언어에서는 내용을 담아 두는 것을 변수(variable)이라고 한다
```java

public class Calcultor{
    public static void main(String[] args) {
        Calcultor calc = new Calcultor();
        
        int a = 10;
        int b = 5;
        System.out.println("add" );
    }
}

```
* 위에 소스에서 변수는 총 4개다 
  * 매개변수 args 인스턴스변수 calc 지역변수 a, b
* 변수는 4가지로 되어있다
  * 지역 변수 (local variable)
    * 중괄호 {} 내에서 선언 된 변수
  * 매개 변수 (parameters)
    * 메소드나 생성자에 넘겨주는 변수
  * 인스턴스 변수 (instance variable)
    * 메소드 밖에, 클래스 안에 선언된 변수, 앞에는 static라는 예약어가 없어야 된다
  * 클래스 변수 (class variable)
    * 인스턴스 변수처럼 메소드 밖에 , 클래스 안에 선언 된 변수 중에서 타입 선언 앞에 static라는 예약어가 있는 변수

* 변수의 종류마다 생명주기가 다르다
   * 지역변수
     * 지역 변수를 선언한 중괄호 내에서만 유효하다
   * 매개변수
     * 메소드가 호출 될 때 생명이 시작되고, 메소드가 끝나면 소멸된다
   * 인스턴스 변수
     * 객체가 생성될 때 생명이 시작되고, 그 객체를 참조하고 있는 다른 객체가 없으면 소멸된다
   * 클래스 변수
     * 클래스가 생성될 때 생명이 시작되고, 자바 프로그램이 끝날 때 소멸 된다
   
 ```
 자바에서는 객체를 더 이상 사용 하지 않으면 가비지 컬렉터가 자동으로 메모리 청소를 해준다
 ```


```java

public class another {

    public void anotherMethod(){
        int localVariable;

        if(true){
            int ex;
        }

        if(true){
            int ex;

        }
        
        if(true){
            int localVariable;  //쓸 수 없다
        }
            
    }
}

```
* ex는 서로 다른 중괄호에 있어 생명주기가 끝나기 때문에 둘 다 쓸 수 있다
* localVariable 를 쓸 수 없는 이유는 맨위에 있는 localVariable의 생명주기가 끝나지 않았기 때문이다 
   * 소스를 컴파일 하면 이미 선언 된 변수이기 때문에 에러가 난다

### 변수이름 정의
 * 길이제한이 없다
 * 첫 문자는 유니코드 문자, 알파벳, $, _ 만 올 수 있다 보통은 $,_ 로 시작하지 않는다
 * 두번째 문자 부터는 유니코드 문자, 알파벳, $, _ 를 쓸 수 있다
 * 보통은 메소드 이름처럼 지정해서 쓴다. 첫 문자는 소문자로 시작하는 단어이고 두번째 단어의 첫 문자만 대문자로 시작한다
 * 상수의 경우에는 모두 대문자로 지정하며, 단어와 단어 사이에는_를 구분한다
   * 계속 값이 변하는 일반적인 변수는 _를 붙이지 않기 바란다
 

### 자료형
* 자료형에는 기본자료형과 참조 자료형으로 나뉘어 진다
* 자바에서 new 예약어를 사용해서 초기화 하는 것을 참조 자료형이라고 한다
   * 예외적으로 String은 String a = "abcd" 이렇게도 되지만 String b = new String("hi"); 이렇게 초기화 할 수 있다
      * String은 new를 쓰지 않고 객체를 생성 할 수 있다

**********
### 기본 자료형
* 기본 자료형은 8개이다
   * 정수형 : byte, short, int, long, char
   * 소수형 : float, double
   * 기타 : boolean