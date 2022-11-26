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
  

1. 부모 클래스에서는 기본 생성자를 만들어 놓는 것 이외에는 상속을 위해서 아무런 작업을 할 필요는 없다.
2. 자식 클래스는 클래스 선언시 extends 다음에 부모 클래스 이름을 적어준다.
3. 자식 클래스에서는 부모 클래스에 있는 public, protected 로 선언된 모든 인스턴스 및 클래스 변수와 메서드를 사용할 수 있다.
4. 자식 클래스에서는 부모 클래스에 있는 public, protected로 선언된 모든 인스턴스 및 클래스 변수와 메서드를 사용할 수 있다.

- 왜 상속이라는 개념이 필요할까?
  - 부모클래스가 갖고 있는 변수와 메서드를 상속 받음으로써, 개발할 때 이중, 삼중의 일을 반복하지 않아도 된다.
  - 변경에 용이하다 .
  
- 자바에서 상속은 다중 상속이 되지 않는다. (단일 상속)

### 상속과 생성자
- 부모 클래스에서는 기본 생성자를 만들어 놓는 것 이외에는 상속을 위해 아무러 작업을 할 필요가 없다.
- 자식 클래스의 생성자가 실행할 때 부모 클래스의 매개 변수가 없는 기본 생성자를 찾는다.
- 매개 변수가 있는 생성자를 만들었을 경우 기본 생성자는 자동으로 만들어지지 않는다.
  - 부모 클래스에 "매개 변수가 없는" 기본 생성자를 만든다.
  - 자식 클래스에서 부모 클래스의 생성자를 명시적으로 지정하는 `super()`를 사용한다.
    - super()?
      - super() 생성자를 사용하면 부모 클래스의 생성자를 호출한다는 것을 의미한다.
      - `super.printName()`을 사용하면 부모 클래스에 있는 `printName()` 메서드를 호출 한다는 의미이다.
    - 자식 클래스에는 지정하지 않아도, 자식 클래스를 컴파일할 때 자동으로 super() 라는 문장이 들어간다.
```java
package c.inheritance;

public class ChildArg extends ParentArg{
    public ChildArg() {
        super("ChildArg");
        System.out.println("Child Constructor");
    }
}
```

- `super("ChildArg")` 라고 자정하면, `ParentArg` 클래스의 생성자 중 `String` 타입을 매개 변수로 받을 수 있는 생성자를 찾는다.  
`String`을 매개 변수로 받는 생성자가 있다면 생성자가 호출된다. 만약 이 생성자처럼 참조 자료형을 매개 변수로 받는 생성자가 하나 더 있다면, `InheritancePrint` 클래스의 객체를 매개 변수로 받는 `ParentArg`생성자가 하나 더 있는 경우를 생각해보자.
```java
package c.inheritance;

public class ParentArg{
    public ParentArg(String name){
        System.out.println("ParentArg("+name+") Constructor");
    }
    public ParentArg(InheritancePrint obj){
        System.out.println("ParentArg(InheritancePrint) Constructor");
    }
    public void printName(){
        System.out.println("printName () - ParentArg");
    }
}
```
- 그러면 ChildArg 클래스의 생성자에서 다음과 같이 `super`에 `null`을 넘겨주면 어떤 객체의 `null`인지 알 수 있을까?
```java
package c.inheritance;

public class ChildArg extends ParentArg{
    public ChildArg(){
        // super("ChildArg");
      super(null);
      System.out.println("Child Constructor");
    }
}
```
- 컴파일 오류가 발생된다.  `reference to ParentArg is ambiguous` 라는 메시지가 있다. 
- 자바는 부모의 매개 변수가 없는 기본 생성자를 찾는 것이 기본
- 부모 클래스에 매개 변수가 있는 생성자만 있을 경우 `super()`를 이용해서 부모 생성자를 꼭 호출해야만 한다.
- 자식 클래스의 생성자에서 `super()`를 명시적으로 지정하지 않으면, 컴파일시 자동으로 `super()`가 추가된다.
- 부모 클래스의 생성자를 호출하는 `super()`는 반드시 자식 클래스의 생성자에서 가장 첫줄에 선언되어야만 한다.


### 메서드 overriding
- Child 클래스의 기능들 ∈ Parent 클래스의 기능들
  - 부모의 기능을 자식이 모두 포함한다.
  - 자식 클래스에서 부모클래스에 있는 메서드와 동일하게 선언하는 것을 메서드 오버라이딩이라고 한다.
  - 접근 제어자, 리턴 타입, 메서드 이름, 매개 변수 타입 및 개수가 모두 동일해야만 메서드 오버라이딩이라고 한다.

```java
package c.inheritance;
public class ParentOverriding {
    public ParentOverriding() {
        System.out.println("ParentOverriding Constructor");
    }
    public void printName(){
        System.out.println("printName() - ParentOverriding");
    }
}
```
```java
package c.inheritance;
public class ChildOverriding extends ParentOverriding {
    public ChildOverriding() {
        System.out.println("ChildOverriding Constructor");
    }
    public void printName() {
        System.out.println("ChildOverriding printName()");
    }
}
```
```java
package c.inheritance;

public class InheritanceOverriding {
  public static void main(String[] args) {
    ChildOverriding child = new ChildOverriding();
    child.printName();
  }
}
```
```
ParentOverriding Constructor
ChildOverriding Constructor
ChildOverriding printName()
```
- 부모 클래스에 선언되어 있는 메서드와 동일하게 선언되어 있는 메서드를 자식 클래스에 선언하면 자식 클래스의 메서드만 실행된다.
- 생성자의 경우 자동으로 부모 클래스에 있는 생성자를 호출하는 `super()`가 추가되지만 메서드는 그렇지 않다. 그것이 바로 메서드 오버라이딩이다.
- 동일하게 선언 되어 있다. = 동일한 시그니처를 가진다.
> 시그니처란? 메서드 이름과 매개변수의 타입 및 개수를 의미한다.
- 리턴 타입도 변경할 수 없다.
- 접근제어자가 확대 되는 것은 문제가 안되지만 축소가 되는 것은 안된다.
> public > protected > package-private > private (오른쪽으로 갈수록 권한 좁아짐)

#### 오버라이딩 정리
- 매서드 오버라이딩은 부모 클래스의 메소드와 동일한 시그니처를 갖는 자식 클래스의 메서드가 존재할 때 성립된다.
- 오버라이딩 된 메서드는 부모 클래스와 동일한 리턴 타입을 가져야만 한다.
- 오버라이딩 된 메서드의 접근 제어자는 부모 클래스에 있는 메서드와 달라도 되지만, 접근 권한이 확장되는 경우에만 허용된다.

#### 오버 로딩/ 라이딩 차이
- 오버 로딩 : 확장 ( 메서드의 매개 변수들을 확장하기 때문에, 확장)
- 오버라이딩 : 덮어 씀 (부모 클래스의 메서드 시그니처를 복제해서 자식 클래스에서 새로운 것을 만들어 내어 부모 클래스의 기능은 무시하고, 자식 클래스에서 덮어씀)

### 참조 자료형의 형 변환
```java
package c.inheritance;
public class ParentCasting {
    public ParentCasting(){
    }
    public ParentCasting(String name){
    }
    public void printName(){
        System.out.println("printName() - Parent");
    }
}
```
- Child 소스
```java
package c.inheritance;
public class ChildCasting extends ParentCasting{
    public ChildCasting(){}
  public ChildCasting(String name){}
  public void printName(){
    System.out.println("printName() - Child");
  }
  public void printAge(){
        System.out.println("printAge() - 18 month");
  }
}
```
- 지금 까지 객체 생성할 때 다음과 같았다.
```
ParentCasting parent = new ParentCasting();
ChildCasting child = new ChildCasting();
```
- 상속관계가 성립되면, 지금까지 객체를 생성한 것과는 다르게, 다음과 같이 객체를 생성할 수도 있다.
`ParentCasting obj = new ChildCasting();`
- 다음은 안된다.
`ChildCasting obj2 = new ParentCasting();`
- 자식 클래스인 `ChildCasting` 클래스에서는 부모 클래스인 `ParentCasting`클래스에서는 사용할 수 있다. 거꾸로 `ParentCasting`클래스에서는 `ChildCasting`클래스에 있는 모든 메서드와 변수들을 사용할 수 없다.
  - 부모 클래스에서는 자식 클래스에 있는 모든 메서드와 변수를 사용할 수도 있고, 그렇지 않을 수도 있다.
  - 만약 자식 클래스에 추가된 메서드나 변수가 없으면 가능할 수도 있다. 만약 자식 클래스에 추가된 메서드나 변수가 없으면 가능할 수도 있다.
  - 하지만 자바 컴파일러에서는 자식 객체를 생성할 때 부모 생성자를 사용하면 안된다고 한다. 명시적으로 형변환을 한다고 알려줘야만 한다.  
  `int` 에서 `long`으로 형 변환이 될 때 별도의 형 변환 작업을 하지 않았던 것을 기억하자. 데이터의 범위가 넓어지므로, 값이 바뀌지 않기 때문이다.  
  하지만 `long`에서 `int` 형 변환을 하려면 값이 바뀔 확률이 있기 때문에, 개발자의 책임하에 명시적으로 형변환은 가능하다.
```
int intValue = 10;
long longValue = 10l;
long casted1 = intValue;
int casted2 = (int) longValue;  
```
동일한 값이 된다는 보장이 전혀 없다. ( 여기서 10이므로 보기에 동일하게 느껴질 수 있으나, longValue 가 int 의 범위를 넘어서면 이 값은 바뀐다.)
참조 자료형은 자식 클래스의 타입을 부모 클래스의 타입으로 형 변환하면 부모 클래스에서 호출할 수 있는 메서드들은 자식 클래스에서도 호출 할 수 있으므로 전혀 문제가 안된다.
따라서 형 변환을 우리가 명시적으로 해줄 필요가 없다.
```java
package c.inheritance;

public class InheritanceCasting {
  public static void main(String[] args) {
    InheritanceCasting inheritance = new InheritanceCasting();
    inheritance.objectCast();
  }
  public void objectCast () {
      ParentCasting parent = new ParentCasting();
      ChildCasting child = new ChildCasting();
      
      ParentCasting parent2 = child;
      ChildCasting child2 = parent;
  }
}
```
- `InheritanceCasting` 클래스를 컴파일하면 `incompatible types` 라는 에러를 내뿜으면서 컴파일이 되지 않는다.  
이유는 `parent` 객체는 `ParentCasting` 클래스의 객체이며, `ChildCasting` 클래스에 선언되어 있는 메서드나 변수를 완전히 사용할 수 없기 때문이다.
```java
package c.inheritance;

public class InheritanceCasting {
  public static void main(String[] args) {
    InheritanceCasting inheritance = new InheritanceCasting();
    inheritance.objectCast();
  }
  public void objectCast () {
      ParentCasting parent = new ParentCasting();
      ChildCasting child = new ChildCasting();
      
      ParentCasting parent2 = child;
      ChildCasting child2 = (ChildCasting)parent;
  }
}
```
- 위는 컴파일은 정상적으로 수행 되나 실행시에 에러가 발생한다.  
실행시에 얘는 원래 `ParentCasting` 클래스의 객체라서 사용할 수 없다라고 예외가 발생한다.
- 언제 이런 명시적은 형 변환을 해도 문제가 없을까? 다음과 같이 기존 메서드를 복사하여 objectCast2() 메서드를 생성해보면
```java
package c.inheritance;

public class InheritanceCasting {
    //중간 생략
  public void objectCast2 () {
      ChildCasting child = new ChildCasting();
      ParentCasting parent2 = child;
      ChildCasting child2 = (ChildCasting) parent2;
  }
}
```
- 아무런 문제 없이 실행이 될 것이다. 왜 아무 문제 없이 실행이 잘 될까,  
마지막 줄에 있는 `parent2`는 어떻게 선언되어 있는 것인지 확인해보자. 
`ParentCasting parent2 = child;`
- `parent2`는 `child`를 대입하였다.  그리고 `child`는 `ChildCasting`클래스의 객체다.
- `parent2`로 겉모습은 `ParentCasting` 클래스의 객체인 것처럼 보이지만, 실제로는 `ChildCasting` 클래스의 객체이기 때문에 `parent2`를 `ChildCasting`클래스로 형 변환을 해도 전혀 문제 없다.
```java
package c.inheritance;

public class InheritanceCasting {
  public static void main(String[] args) {
    inheritanceCasting inheritance = new InheritanceCasting();
    //inheritance.objectCast();
    //inheritance.objectCast2();
    inheritance.objectCastArray();
  }
  //중간 생략
  public void objectCastArray() {
      ParentCasting[] parentArray = new ParentCasting[3];
       parentArray[0] = new ChildCasting();
       parentArray[1] = new ParentCasting();
       parentArray[2] = new ChildCasting();
  }
}
```
- `ParentCasting` 배열은 3개의 값을 저장할 수 있는 공간을 가진다.  
그런데, 0번째 배열과 2번째 배열은 `ChildCasting`클래스의 객체를 할당한 것을 볼수 있다. 문제는 없다.  
이와 같이 일반적으로 여러 개의 값을 처리하거나, 매개 변수로 값을 전달할 때에는 보통 부모 클래스의 타입으로 보낸다.  
이유는 배열과 같이 여로 값을 한번에 보낼 때 각 타입별로 구분해서 메서드를 만들어야 하는 문제가 생길 수도 있기 때문이다.
- `parentArray`라는 배열의 타입이 `ChildCasting`인지 `ParentCasting`인지 구분할 때 쓰는 것이 `instanceof`라는 예약어다.
이 `objectCastArray()` 메서드에 `instanceof`를 사용하여 타입을 구분하는 `objectTypeCheck()`라는 메서드를 같이 확인해보자.
```java
package c.inheritance;

public class InheritanceCasting {
  public static void main(String[] args) {
    inheritanceCasting inheritance = new InheritanceCasting();
    //inheritance.objectCast();
    //inheritance.objectCast2();
    inheritance.objectCastArray();
  }
  //중간 생략
  public void objectCastArray() {
      ParentCasting[] parentArray = new ParentCasting[3];
       parentArray[0] = new ChildCasting();
       parentArray[1] = new ParentCasting();
       parentArray[2] = new ChildCasting();
       objectTypeCheck(parentArray);
  }
  
  private void objectTypeCheck(ParentCasting[] parentArray){
      for (ParentCasting tempParent: parentArray){
          if (tempParent instanceof ChildCasting){
              System.out.println("ChildCasting");
          }else if(tempParent instanceof ParentCasting) {
              System.out.printl("ParentCasting");
          }
      } 
  }
}
```
- `instanceof`의 앞에는 객체를 뒤에는 클래스(타입)를 지정해 주면 boolean 타입으로 결과 제공.
- instanceof 로 타입 확인 후 명시적으로 형 변환시 문제를 줄일 수 있다.
- instanceof를 사용하면 정확하게 타입을 확인할 수 있고, 원하는 메서드도 호출할 수 있다.
  - instanceof 사용시 유의점
    - instanceof로 타입을 점검할 때 ParentCasting의 인스턴스인지 여부를 먼저 점검하면 안된다.
    - parentCasting 으로 먼저 확인하여 결과 값이 고정되기 때문.
    - 타입 점검 시에는 가장 하위에 있는 자식 타입부터 확인을 해야 제대로 타입 점검이 가능
      - 참조 자료형도 형변환이 가능하다.
      - 자식 타입의 객체를 부모 타입으로 형 변환 하는 것은 자동으로 된다.
      - 부모 타입의 객체를 자식 타입으로 형 변환을 할 때에는 명시적으로 타입을 지정해 주어야 한다.
        - 부모 타입의 실제 객체는 자식 타입이어야만 한다.
        - instanceof 예약어를 사용하면 객체의 타입을 확인할 수 있다.
        - instanceof 로 타입 확인시에는 부모 타입도 true라는 결과를 제공한다.
### Polymorphism
 - Polymorphism = 다형성
 - Child 클래스를 복사한 후 printName() 메서드의 내용과 클래스 선언부, 생성자 선언부만 변경하면 된다.
 - Parent 클래스의 자식 클래스가 두 개 이상, 개수에 제한은 업삳.
 - 상속 받은 자식 클래스 호출시 부모 클래스의 기본 생성자 호출, 이후 자식 본인의 생성자 호출 후 메서드등 실행.
 - 형 변환을 하더라도 실제 호출된 메서드는 생성자를 사용한 클래스에 있는 것이 호출된다. 
   - 각 객체의 실제 타입은 다르기 때문. " 형 변환을 하더라도, 실제 호출되는 것은 원래 객체에 있는 메서드가 호출된다."

### 자식 클래스에서 할 수 있는 일들을 다시 정리해보자
- 자식 클래스의 생성자가 호출되면 자동으로 부모 클래스의 매개 변수가 없는 기본 생성자가 호출된다. 명시적으로 super() 라고 지정할 수도 있다.
- 부모 클래스의 생성자를 명시적으로 호출하려면 super()를 사용하면 된다.
- 변수 관련된 내용들은 다음과 같다.
  - 부모 클래스에 `private` 로 선언된 변수를 제외한 모든 변수가 자신의 클래에 선언된 것처럼 사용할 수 있다.
  - 부모 클래스에 선언된 변수와 동일한 이름을 가지는 변수를 선언할 수도 있다. 하지만 권장되지 않는다.
  - 부모 클래스에 선언되어 있지 않은 이름의 변수를 선언할 수 있다.
- 메서드 관련된 내용
  - 변수처럼 부모 클래스에 선언된 메서드들이 자신의 클래스에 선언된 것처럼 사용할 수 있다.
  - 부모 클래스에 선언된 메서드와 동일한 시그니처를 사용함으로써 메서드를 overriding할 수 있다.
  - 부모 클래스에 선언되어 있지 않은 이름의 새로운 메서드를 선언할 수 있다.
  

### Overriding과 Overloading은 복제와 확장의 개념이다.