# 참조 자료형에 대해서 알아보자
## 참조 자료형은 나머지 전부이다.
- 기본 자료형 8개(`byte`, `shor`, `int`, `long`, `float`, `double`, `char`, `boolean`)를 제외한 나머지 타입은 모두 참조 자료형`Reference type`이다.
- 기본 자료형과 참조 자료형의 가장 큰 차이는 new를 사용해서 객체를 생성하는지 여부의 차이이다.  
new 없이도 객체를 생성할 수 있는 참조 자료형은 오직 `String`뿐이라고 알고 있으면 된다.
- 각종 연산자들은 대부분 기본 자료형을 위해서 존재한다.
- 그중에서 +는 참조 자료형 중에서 `String`클래스만 사용 가능하고, 나머지 클래스에서는 사용할 수 없다.
- `String`을 제외한 다른 참조 자료형이 사용할 수 있는 연산자는 오직 하나 `=` 등호이다.
- 참조 자료형을 if 같은 조건문 `while` 이나 `for` 와 같은 반복문에서 그냥 사용할 수는 없다.  
해당 자료형에서 제공하는 메서드에서 `boolean`타입의 리턴 값을 제공하면 사용할 수는 있다.
- `null`인지 체크하는 경우는 이러한 조건문이나 반복문을 사용할 수 있다.
> switch문에서 사용할 수 있는 참조 자료형도 `String`뿐인데 , 이 `String`도 `JDK 7 이상의 버전에서만 사용 가능하다.

### 기본 생성자
- 자바는 생성자를 만들지 않아도 자동으로 만들어지는 기본 생성자가 있다.  
> main() 메서드에서 실습 클래스의 이름으로 객체를 생성한 것이 바로 기본 생성자다.
```java
public class ReferenceDefault {
    public static void main(String[] args) {
        ReferenceDefault reference = new ReferenceDefault();
    }
}
```
- `main()` 메서드를 보면 `ReferenceDefault`클래스의 인스턴스인 `reference`를 만들었는데, 여기서 등호 우측에 `new` 옆에 있는 `ReferenceDefault()`것이 생성자다.  
하지만 소스는 보이지 않다. 이와 같이 아무런 매개 변수가 없는 `ReferenceDefault()`라는 생성자는 다른 생성자가 없을 경우 기본으로 컴파일할 때 만들어진다.
  
- 아래와 같이 `String`을 매개 변수로 받는 `ReferenceString`이라는 클래스를 보자.
```java
public class ReferenceString{
    public ReferenceString(String arg){
        
    }

    public static void main(String[] args) {
        ReferenceString reference = new ReferenceString();
    }
}
```
- 생성자는 메서드와 비슷하게 생겼지만, 리턴 타입이 없고, 클래스 이름으로 되어 있다는 점이 메서드와 다르다.
- 이렇게 `String`을 매개 변수로 받는 `ReferenceString`이라는 클래스를 만들고 컴파일 하면 정상적으로 컴파일이 될까? - 오류가 발생한다.
```
$ javac ReferenceString.java
ReferenceString.java:9: error: constructor ReferenceString in class ReferenceString cannot be applied to given types;
    ReferenceString reference = new ReferenceString();
    
    required: String
    found: no argments
    reason : actual and formal argument lists differ in length
    
1 error
```
- `actual and formal argument lists differ in length`이란는 컴파일 오류가 발생한다.
  - 기본 생성자에 대한 설명에서 "아무런 매개 변수가 없는 ReferenceString()"이라는 생성자는 다른 생성자가 없을 경우 기본으로 컴파일 할 때 만들어진다."라고 되었다.  
    그런데 기본 생성자는 다른 생성자가 있으면 자동으로 만들어지지 않는다. 그러면 매개 변수가 없는 생성자를 사용하고 싶으면 어떻게 해야 할까

```java
public class ReferenceString {
  public ReferenceString(){}
  public ReferenceString(String arg){}

  public static void main(String[] args) {
    ReferenceString referenceString = new ReferenceString();
  }
}
```
- 위와 같다면 컴파일 오류는 피할 수 있다.

- 자바에서 생성자는 왜 필요할까
자바의 생성자는 자바 클래스의 객체(또는 인스턴스)를 생성하기 위해서 존재한다.  
  방금 살펴 본 main() 메서드에서 referenceString 이라는 것이 바로 객체다.
  - 메서드와 비슷하다.
  - 선어부에 리턴 타입이 없다.
  - 메서드의 이름 대신 클래 이름과 동일하게 이름을 지정하는 것 뿐이다.
  - 생성자에 리턴 타입이 없는 이유는 생성자의 리턴 타입은 클래스의 객체이기 때문이다.
  - 클래스와 이름이 동일해야 컴파일러가 생성자인 것을 인식한다.
  - 보통은 가장 윗부분에 선언한다.
  
```java
public class ReferenceString{
    String instanceVariable; // 인스턴스 변수
  public ReferenceString() {}     // 생성자 영역
  public ReferenceString(String arg){} // 생성자 영역

  public static void main(String[] args) {   // 메서드 영역
    ReferenceString reference = new ReferenceString();
  }
  public String getString(){ // 메서드 영역
      return instanceVariable;
  }
  public void setString(String str){ //메서드 영역
      instanceVariable = str;
  }
}
```
- 즉, 인스턴스 변수들을 선언한 후에 생성자를 위치시키고, 그 다음에 여러분들이 피룡한 메서드들을 위치시켜야 누가 해당 소스 코드를 보더라도 생성자를 찾기 위한 시간을 허비하지 않을 것이다.    
그렇다고 메서드가 클래스 선언 바로 다음에 선언되어 있고, 그 밑에 생성자가 있으면 컴파일이 안되거나 하는 문제가 발생하지 않는다.  
일반적인 대부분의 코드들은 이러한 암묵적인 약속하에 작성하기 때문에, 약속을 지키는 것이 좋다.  
  만약 생성자가 없는 클래스는 객체를 생성할 없는 것은 아니다. 생성자가 없더라도 객체를 얻을 수 있는 클래스도 있다.
  
### 생성자는 몇 개까지 만들 수 있을까
- 자바는 클래스의 객체를 보다 간편하게 만들기 위해 여러 가지 매개 변수를 갖는 여러 생성자를 가질 수 있다.  
생성자의 개수는 상관 없다.
  - 예시로 어떤 속성을 갖는 클래스를 만들고 그 속성들을 쉽게 전달하기 위해 DTO라는 것을 만든다.
  > VO는 데이터를 담아 두기 위한 목적으로 사용, DTO는 데이터를 다른 서버로 전달하기 위한 것이 주 목적이다. (DTO가 VO를 포함할 수도 있다.)
  - name, phone, email 이라는 인스턴스 변수를 갖는 MemberDTO
```java
public class MemeberDTO{
    public String name;
    public String phone;
    public String email;
}
```
- 이렇게 DTO를 만들어두는 이유 
  - 자바의 메서드를 선언할 때 리턴 타입은 한가지만 선언할 수 있다.  
  이와 같은 복합적인 데이털르 리턴하려면 String[] 과 같이 배열을 리턴해도 되지만, `int`타입등을 포함하면 애매해진다.  
  그래서 이처럼 DTO를 만들어 놓으면 메서드의 리턴 타입에 `MemberDTO`로 선언하고, 그 객체를 리턴해 주면 된다.
```java
public MemeberDTO getMemberDTO(){
    MemberDTO dto = new MEmberDTO();
    //중간 생략
        return dto;
        }
```
- 각각 name만 알지도, phone만 알수도, email만 알수도 혹은 두개씩만 알 수도 있는 여러 상황이기 때문에.
오버로딩 하여 기본 생성자를 생성할 수 있기 때문에 개수는 상관이 없다. 하지만 필요에 맞는 생서자만 만드는 습관을 들여아한다.  
매개 변수가 없는 생성자르 제외하고 모두 `this`라는 예약어가 사용된 것을 볼 수 있다.  
  이 예약어를 변수에 사용할 때에는 객체의 변수와 매개 변수의 이름이 동일할 때, 인스턴스의 변수를 구분하기 위해서 사용한다.
  
- 생성자에도 오버로딩 하여 사용 가능.

### 이 객체의 변수와 매개 변수를 구분하기 위한 this
- `this` 라는 예약어는 영어 단어의 의미 그대로 "이 객체" 의 의미다.

### 메서드 Overloading
- 클래스의 생성자는 매개 변수들을 서로 다르게 하여 선언할 수 있다.
- 그렇다면 메서드도 이렇게 이름은 같게 하고 매개 변수들을 다르게 하여 만들 수 있다.
- 메서드들은 모두 이름이 동일하지만, 각 메서드의 매개 변수의 종류와 개수 순서가 다르다.
  - 첫 번째 `print()` 메서드는 `int`를 매개 변수로
  - 두 번째 `print()` 메서드는 `String`을 매개 변수로 하고 있다.
  - 세 번째 메서드와 네 번째 메서드를 보면 각 매개 변수들의 이름은 같지만, 세 번째 메서드는 `int`,`String` 순서이며, 네 번째는 `String` `int`순이다.
  - 개수가 같아도 타입의 순서가 다르면 다른 메서드이다.
  - 중요한 것은 매개 변수의 이름이 아니라 매개 변수의 타입이다.   
    타입이 다르면 다른 메서드로 생각하지만, 타입이 같고 변수 이름이 같으면 같은 메서드로 인식한다.
    
- 같은 역할을 하는 메서드는 같은 메서드 이름을 가져야 한다. 생성자도 매개 변수에 따라서 다르게 인식된다.\

### 메서드에서 값 넘겨주기
#### 메서드의 수행과 종료에 대해 알아보자.
- 메서드가 종료되는 조건
  - 메서드의 모든 문장이 실행되었을 때
  - return  문장에 도달 했을 때
  - 예외가 발생(throw) 했을 때
  
- 모든 타입을 한개만 리턴 타입으로 넘겨줄 수 있다.
- 모든 기본 자료형과 참조 자료형 중 하나를 리턴할 수 있다.
  - `int`만 리턴, `int`의 배열을 리턴, `String`을 리턴
    - 메서드 이름 앞에 변수의 타입을 지정해 주고
    - 메서드 내에서는 그 타입을 생성하고 가공한 후
    - `return` 이라는 예약어를 사용하여 리턴해주 면 
    - 요청한 메서드로 그 값이 전달된다.
  
- `return` 이라는 예약어를 사용하여 메서드를 리턴하면 그 메서드는 값을 넘겨주고 그 위치에서 종료한다.
- 여러 값을 넘겨주려면  DTO 를 사용해서 리턴타입으로 지정하여 사용하면 된다.
- `void`인 메서드에서는 `return`뒤에 아무것도 없이 바로 세미콜론을 적어주면, "메서드 수행을 종료해라."라고 인식한다.

## static 메서드와 일반 메서드 차이
- `System.out.println()`메서드는 왜 겍체를 생성하지 않아도 될까 ? 이것이 `static` 예약어 이기 때문이다.
`static`은 객체를 생성하지 않아도 메서드를 호출 할 수 있다.
```java
public class ReferenceStatic{
  public static void main(String[] args) {
    ReferenceStatic.staticMethod();
  }
  
  public static void staticMethod(){
      System.out.println("This is a staticMethod");
  }
}
```
- `static` 메서드는 클래스 변수만 사용할 수 있다는 단점이 있다.   
  staticMethodCallVariable()이라는 메서드를 다음처럼 사용할 수 있다.
  

```java
public class ReferenceStatic{
    String name = "Min";
    //중간 생략
  public static void staticMethodCallVariable(){
      System.out.print(name);
  }
} 
```
- 이는 컴파일이 되지 않는다. => `static`이 아닌 변수 이름은 `static context`에서 참조할 수 없다.
  - `staticMethod()` 의 선언에 `static`을 빼는 방법이다. 그러려면 `staticMethod()`메서드를 참조하는 모든 메서드에서 `ReferenceStatic`의 객체를 생성한 후 `staticMethod()`를 호출해야만 한다.
  - 다른 한 가지 방법은 `ReferenceStatic`의 `name`이란느 변수 선언시 `static`으로 선언해야 한다. 다음과 같이 `String`앞에 `static`을 붙여주면 된다.
  
```
public static String name;
```
- `name`을 `static`으로 선언하게 되면 이 `name`은 인스턴스 변수가 아닌 클래스 변수가 된다.   
이렇게 아무 생각 없이 인스턴스 변수에 `static`을 붙이면 여러분들이 예상치도 못한 상황이 발생하게 된다.
- `static`을 붙이면 모든 객체에서 하나의 값을 바라보기 때문이다.
```java
public class ReferenceStaticVariable{
    static String name;
    public ReferenceStaticVariable(){}
  public ReferenceStaticVariable(String name){
        this.name = name;
  }

  public static void main(String[] args) {
    ReferenceStaticVariable reference = new ReferenceStaticVariable();
    reference.checkName();
  }
  
  public void checkName(){
        ReferenceStaticVariable reference1 = new ReferenceStaticVariable("SangMin");
        System.out.println(reference1.name);
        ReferenceStaticVariable reference2 = new ReferenceStaticVariable("Sungchoon");
        System.out.println(reference1.name);     
  }
}
```
```
SangMin
Sungchoon
```
- ReferenceStaticVariable의 `name`이라는 변수가 인스턴스 변수가 아닌 `static`으로 선언한 클래스 변수이기 때문이다.
  ReferenceStaticVariable의 name 선언부에서 `static`을 제거하고 컴파일 을 다시 하면 둘 다 `SangMin`으로 출력된다.
  
## static 블럭
- `static`에 대해서 설명한 김에 `static`을 특이하게 사용하는 방법을 한 가지 더 살펴보자.
- 어떤 클래스의 객체가 생성되면서 딱 한번만 불려야 하는 코드가 있다고 생각해 보자.
- 객체는 여러 개를 생성하지만, 한 번만 호출되어야 하는 코드가 있다면 `static`블럭을 사용하면 된다.
```
static {
//딱 한번만 수행되는 코드
}
```
이 `static`블럭은 객체가 생성되기 전에 한 번만 호출되고, 그 이후에는 호출하려고 해도 호출할수가 없다.
그리고, 클래스 내에 선언되어 있어야 하며, 메소드 내에 서는 선언할 수가 없다.
즉, 인스턴스 변수나 클래스 변수와 같이 어떤 메서드나 생성자에 속해있으면 안 된다.
```java
public class StaticBlock{
    static int data = 1; 
    public StaticBlock(){
        System.out.println("StaticBlock Constructor. ");
    }
    
    static{ 
        System.out.println("*** First static block. ***");
        data = 3;
    }
    
    static {
        System.out.println("*** Second static block. ***");
        data = 5;
    }
    
    public static int getData(){
        return data;
    }
}
```
일단은 이 예제 코드에서 `data`라는 값은 신경 쓰지 말. System.out.println() 메서듣르만 살펴보자.
이 StaticBlock 클래스에는 두개의 `static`블럭이 선언되어 있다. `static`블록은 이처럼 여러개를 선언할 수 있으며 선언되어 있는 순서는 매우 중요하다.
왜냐하면, 선언된 순서대로 블록들이 차례로 호출되기 때문이다.
이 `StaticBlockCheck` 클래스를 다음과 같이 만들자.

```java
public class StaticBlockCheck{
  public static void main(String[] args) {
    StatikcBlock check = new StaticBlockCheck();
    check.makeStaticBlockObject();
  }
  
  public void makeStaticBlockObject(){
      System.out.print("Creating block1");
      StaticBlockCheck block1 = new StaticBlockCheck();
      System.out.print("Created block1");
      System.out.print("--------------");
      System.out.print("Creating block2");
      StaticBlockCheck block2 = new StaticBlockCheck();
      System.out.print("Created block2");
  }
}
```
- 두 개의 `StaticBlock` 객체를 만들었으며, 호출되는 순서를 살펴보기 위해서 객체 생성 전, 후에 출력문을 추가해 두었다.

```
Creating block1
*** First staic block. ***
*** Second static block. ***
StaticBlock Constructor.
Created block1
---------------------
Creating block2
StaticBlock Constructor.
Created block2
```
두 개의 StaticBlock 객체를 만들었지만, static 블록들은 단지 한번씪만 호출되었다.
게다가, 생성자가 호출되기 전에 `static` 블록들이 호출된 것을 볼 수 있다.
이와 같은 `static`블록은 클래스를 초기화할 때 꼭 수행되어야 하는 작업이 있을 경우 유용하게 사용될 수 있다.
추가로, `static` 블록 안에서는 `static`한 것들만 호출할 수 있다.
`StaticBlock` 클랙스를 살펴보면 `static`블록 안에서 사용한 `data`라는 값은 `static`으로 선언되어 있기 때문에 사용이 가능한 것이다.
`data`변수 선언에 있는 `static` 예약어를 없앤다면, 이 클래스는 컴파일이 되지 않는다.
다음과 같이 `makeStaticBlockObjectWithData()`  메서드를 만들어 `data`의 값을 확인해보자.
```java
public class ata{
    

public void makeStaticBlockObjectWithData(){
    System.out.println("data=" + StaticBlock.getData());
    StaticBlock block1 = new StaticBlock();
    block1.data = 1;
    System.out.print("--------");
    StaticBlock block2= new StaticBlock();
    block2.data =2;
    System.out.print("data= " + StaticBlock.getData());
        }
}
```
 `StaticBlockChekc` 클래스의 `main()` 이 메서드만 호출되도록 변경해야만 결과가 동일하게 나온다.
 가장 먼저 data 값이 출력되기 전에 static 블록들이 호출되어 두 줄의 결곽를 먼저 출력ㅎ하는 것을 볼 수 있다. <br>
 클래스에 대한 참조가 발생하잠자ㅏ 호출되는 것을 알 수 있다. 그리고 앞서 한번 설명했지만, 복습 차원에서 `data`의 값이 어떻게 바뀌었는지 확인해 보자.
`static` 블록에 `data`처럼 .`static` 변수만 사용할 수 있는 아니고, `getData()` 와 같이 `static`으로 선언된 메서드도 호출할 수 있다.
궁금하다면 직접 코드를 변경하여 확인해 보기 바란다. `static` 블록을 여러분들이 쓸 일은 그리 많지 않지만, 가뭄에 콩 나듯이 가끔 사용할수도 있으니 꼭 기억하고 있어야 한다.

### 매개 변수를 지정하는 특이한 방법
- 매개 변수가 몇 개가 될지, 호출할 때마다 바뀌는 경우에는 어떻게 해야 할까,
  - 다음과 같이 배열을 넘겨주는 방법. (타입이 동일해야함.)
  - 자바에서는 임의 개수의 매개 변수(Arbitrary Number of Arguments)를 넘겨줄 수 있는 방법을 제공.
  - `타입... 변수명` 으로 선언해 주면, `numbers`는 배열로 인식하고 그 값은 다음과 같이 처리할 수 있다.
  여기서 중요한 것은 ...을 적어줄 때에 점을 연속해서 적어줘야지, 점 사이에 공백이 있으면 안 된다.