## 3장 객체란 무엇인가
******

### * 자바는 객체지향 언어라고 한다
* 자바는 객체지향 언어이다
  * 모든 사물들은 객체로 되어있다.
  * 물리적으로 존재하는 것들 (사람, 책상, 노트북) 과 추상적인 존재 (주문, 수업) 을 객체로 볼 수 있다
  * 모든 사물에는 상태(state)와 행위(behavior)가 있다.  
    * ex) 시속 150km/h 로 이동 중 인 상태, 800km를 주행한 상태, 정지중인 상태  
    가속을 하는 행위, 브레이크를 거는 행위 
  * 사물을 객체로 나눌 수 있으며 행위를 찾아낼 수 있다


  ```java
  public class Car{
    
    public Car(){
        
    } // 생성자
  
  int speed = 100;
  int distance = 800;
  String color = "black";
 // int는 정수 String 문자열

  public void speedUp(){
      
  }

  public void breakDown(){

  }
}

```
* 위 Car 클래스의 속도 이동거리 색상 등을 다음과 같이 변수로 나타낼 수 있다
* 변수를 지정함으로써 클래스의 상태를 정할 수 있다
* 속도를 올리는 speedUp()과 속도를 줄이는 breakDown()는 메소드로 클래스의 상태를 변경하는 행위를 지정 할 수 있다

### 클래스와 객체는 구분해야 된다
* 각각의 실제를 나타내기 위한 것을 객체(Object) 또는 인스턴스(Instance)라고 한다

```java
  public class CarManager{
  public static void main(String[] args) {
    Car dog = new Car(); // dog라는 객체 생성
    Car cow = new Car(); // cow라는 객체 생성
  }
 
}
```
* 위의 Car()는 생성자(constructor)라고 한다 
* 생성자는 객체를 생성하기 위한 유일한 도구이다
* 매배 변수가 없는 생성자를 기본생성자 라고 하며 클래스를 컴파일 할 때 javac에서 자동으로 만들어 준다
* new 라는 것은 예약어 중 하나이며 new를 통해서 생성자를 호출하면 객체가 생성된다
* 클래스는 자체만으로 일을 할 수 없고 객체를 생성해야만 일을 시킬 수 있다
  * dog차의 속도를 높이고 싶으면 dog객체를 만들고 그 객체의 메소드를 호출하면 된다
  * 메소드 호출은 dog.speedUp()  객체이름.메소드이름

```java
  public class Car{

  public Car(){

  } // 생성자

  int speed;
  int distance;
  String color;
  // int는 정수 String 문자열

  public void speedUp(){
    speed = speed +5;
  }

  public int breakDown(){
    speed = speed - 10;
    return speed;
  }
  
}
 
}
```
 * 완성 된 Car 클래스를 갖고 속도를 증감 시키는 CarManger 만든다
```java
  public class CarManger{

  public static void main(String[] args) {
      Car dog = new Car(); // 객체 생성 
      dog.speedUp();
      dog.breakDown();
    
  }
}
 
}
```
* Car 클래스를 컴파일 하지 않고 CarManger 클래스만 컴파일 하더라도 문제되지 않는다 
  * CarManger 클래스에서 Car 클래스를 참조하기 때문에 Car 클래스도 같이 컴파일 된다


### 객체 생성
 ```java
  public class Calculator{

  public static void main(String[] args) {
    System.out.println("Calculator class");
    Calculator calc = new Calculator(); // 객체생성
    
    int a = 10;
    int b = 5;
    calc.add(a,b);
    calc.subtract(a,b);
    calc.multiply(a,b);
    calc.divide(a,b);
  }
  
  public int add(int a, int b){
      return a+b;
  }
  public int subtract(int a, int b){
    return a-b;
  }
  public int multiply(int a, int b){
    return a*b;
  }
  public int divide(int a, int b){
    return a/b;
}
```
* 객체를 생성하기 위해서는 클래스 객체이름 = new 클래스();
  * Calculator 클래스는 생성자가 없어도 자동으로 기본생성자를 생성해준다

### 정리
* 객체란 물리적이나 추상적으로 가질 수 있으며 상태(변수)와 행위(메소드)가 있다
* 클래스 자체만으로 일을 할 수 없고 객체를 생성해야지 일을 할 수 있다
* 객체를 만들기 위해서는 new 예약어와 클래스 이름과 동일한 생성자를 호출하여 만든다
