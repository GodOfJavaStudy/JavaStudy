# 10장 자바는 상속이라는 것이 있어요.
## 자바에서 상속이란?
```java
package  c.inheritance;

public class Parent {
    public Parent() {
        System.out.println("Parent Constructor");
    }
    public void printName(){
        System.out.println("Parent printName()");
    }
}
```
```java
package  c.inheritance;
public class Child extends Parent {
    public Child() {
        System.out.println("Child Constructor");
    }
}
```
- `extends`는 자바의 예약어 상속 받는다는 뜻.
- 부모 클래스에 선언되어 있는 `public` 및 `protected`로 선언되어 있는 모든 변수와 메서드를 내가 갖고 있는 것처럼 사용 가능.
> UML : Unified Modeling Language 의 약자 . 
> Class Diagram, Sequence Diagram, Use Case Diagram 등이 존재한다.
> 클래스 다이어그램에서 속이 빈 삼감형으로 화살표로 가리키면 자식 -> 부모 클래스를 가리키는 상속 관계를 나타낸다.
> 상속 관계가 아니라면 그냥 직선으로 관계를 나타낸다.

```java
package  c.inheritance;

public class InheritancePrint {
    public static void main(String[] args) {
        Child child = new Child();
        child.printName();
    }
}
```
```
Parent Constructor
Child Constructor
Parent printName()
```
- `Parent` 클래스의 메서드를 호출하지도 않았는데, 확장을 한 클래스가 생성자를 호출하면, 자동으로 부모 클래스의 기본 생성자(매개 변수가 아무것도 없는 생성자)가 호출된다.  
다음 자식 클래스의 생성자에 있는 내용들이 수행된다. 
  

1. 부모 클래스에서는 기본 생성자를 