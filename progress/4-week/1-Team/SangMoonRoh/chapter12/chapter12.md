# 모든 클래스의 부모 클래는 Object에요

## 모든 자바 클래스의 부모인 java.lang.object 클래스
- 모든 클래스의 부모 클래스 Object

```java
package c.inheritance;

public class InheritanceObject{
    public static void main(String[] args) {
        InheritanceObject object = new InheritanceObject();
        System.out.println(object.toString());
    }
}
```

- 자바에서는 기본적으로 이렇게 아무런 상속을 받지 않으면 java.lang.Object 클래스를 확장한다.
    - `Object` 클래스에 있는 메서드를 사용해보면 알 수 있다. 위의 코드에서 `toString()` 이라는 메서드가 호출된 것을 볼 수 있다.
- `extends`를 사용하여 부모 클래스를 상속 받을 때에는
    - 자바는 이중 상속을 받을 수 없지만, 여러 단계로 상속을 받을 수는 있다.
    - `Object` < Parent < Child
- 왜 모든 클래스는 Object 클래스의 상속을 받을까,
  - Object 클래스에 있는 메서드들을 통해서 클래스의 기본적인 행동을 정의할 수 있기 때문이다.
    - ex) 사람은 두발로 걷고 말을 하고 생각을 한다.와 마찬가지로 클래스라면 "이 정도의 메서드는 정의되어 있어야 하고,처리 해주어야 한다."는 것을 정의하는 작업이 필요하기 때문에 `Object`클래스를 상속 받는다.
    - `Object` 클래스에는 `toString()`외에 어떤 메서드들을 자동 상속 받을까
  
### Object 클래스에서 제공하는 메서드들의 종류는?
- Object 클래스에 선언되어 있는 메서드는 객체를 처리하기 위한 메서드와 쓰레드를 위한 메서드로 나뉜다.
> 쓰레드 라는 것은 "프로그램이 실행되는 작은 단위 중 하나"
> 웹 어플리케이션 서버처럼 사용자들의 요청들을 동시에 받기 위해서는 여러 개의 쓰레드가 동작하여야만 정상적으로 동작할 수 있다.

- 자바에서 메서드를 표현할 때에는 보통 여기에 정리된 것과 같이 "접근 제어자 리턴 타입 메서드이름 (매개변수)"순으로 나열.

|메서드|설명|
|--------------|-------------|
|protected Object clone() | 객체의 복사본을 만들어 리턴한다.|
|public boolean equals(Object obj) | 현재 객체와 매개 변수로 넘겨받은 객체가 같은지 확인한다. 같으면 `true`를 다르면 `false`를 리턴한다.|
|protected void finalize()|현재 객체가 더 이상 쓸모가 없어졌을 때 가비지 컬렉터(`garbage collector`)에 의해서 이 메서드가 호출된다. |
|public Class<?> getClass() | 현재 객체의 Class 클래스의 객체를 리턴한다. |
|public int hashCode|객체에 대한 해시 코드(hash code) 값을 리턴한다. 해시 코드라는 것은 "16진수로 제공 되는 객체의 메모리 주소" 를 말한다.|
|public String toString()|객체를 문자열로 표현하는 값을 리턴한다.|

- 쓰래드 처리르 위한 메서드

|메서드|설명|
|public void notify()| 이 객체의 모니터에 대기하고 있는 단일 쓰레드를 꺠운다.|
|public void notifyAll()| 이 객체의 모니터에 대기하고 있는 모든 쓰레드를 깨운다.|
|public void wait() | 다른 쓰레드가 현재 객체에 대한 `notify()` 메서드나 `notifyAll()`메서드를 호출할 때까지 현재 쓰레드가 대기하고 있도록 한다.|
|public void wait(long timeout)| `wait()`메서드와 동일한 기능을 제공하며,매개 변수에 지정한 시간 만큼만 대기한다. 여기서의 시간은 밀리초로 1/1,000초 단위이다. 만약 1초간 기다리게 할 경우에는 1000을 매개 변수로 넘겨주면 된다.
|public void wait(long timeout,int nanos)|`wait()` 메서드와 동일한 기능을 제공한다. 하지만. wait(timeout)에서 밀리초 단위의 대기 시간을 기다린다면, 이 메서드는 보다 자세한 밀리초 + 나노초 (1/1,000,000,000초) 만큼만 대기한다. 뒤에 있는 나노초의 값은 0~999,999사이의 지정 값만 지정할 수 있다.

### Object 클래스에서 가장 많이 쓰이는 toString()  메서드
- toString()
- equals()
- hashCode()
- getClass()
- clone()
- finalize()

- toString이 호출되는 경우
  - System.out.println() 메서드에 매개 변수로 들어가는 경우
  - 객체에 대하여 더하기 연산을 하는 경우
  
```java
package c.inheritance;

public class ToString{
  public static void main(String[] args) {
    ToString thisObject = new ToString();
    thisObject.toStringMethod(thisObject);
  }
  public void toStringMethod(Object obj){
      System.out.println(obj);
      System.out.println(obj.toString());
      System.out.println("plus " + obj);
  }                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              
} 
```
- toStringMethod() 메서드의 가장 첫 줄에서는 객체를 그대로 출력,
- 두번째 줄에서, toString() 메서드를 호출.
- ToString 클래스에 전혀 선언되어 있지 않다.  
- ToString 클래스는 Object 클래스의 상속을 자동으로 받는다.  
toString() 메서드는 Object 클래스에 선언되어 있기 때문에, 이렇게 toString() 메서드를 호출해도 문제가 되지 않음.
- 마지막 줄에서는 객체의 더하기 연산을 수행한다.
참조 자료형의 더하기 연산은 String 만 가능하다.(일반적인 객체 더하기 제외)

```java
public void toStringMethod2() {
    System.out.println(this);
    System.out.println(toString());
    System.out.println("plus" + this);
        }
```

- this 키워드를 사용하면 자기 자신을 나타내는 객체를 안넘겨 주어도 된다.
- toString() 으로 출력된 결과
  - `getClass().getName() + '@' + Integer.toHexString(hashCode())`
  - Object 클래스에 있는 getClass() 의 결과에 getName() 메서드를 부르면 현재 클래스의 패키지 이름과 클래스 이름이 나온다. 
  - at('@')는 앞의 결과와 뒤의 결과를 구분하기 위한 구분자이다.
  - 마지막 부분에는 객체의 해시 코드 값을 출력한다. hashCode() 메서드에서는 int 타입의 값을 리턴해준다. 그 값을 Integer 라는 클래스에서 제공하는 toHexString()  이라는 메서드를 활용하여 16진수로 변환하는 작업이 수행된다.
  
- ToString 클래스의 toString() 메서드를 Overriding
```java
package c.inheritance;

public class ToString{
  public static void main(String[] args) {
    ToString thisObject = new ToString();
    thisObject.toStringMethod(thisObject);
  }
  
  public String toString (){
      return "ToString class";
  }
}
```

```
ToString class
ToString class
plus ToString class
```

- `toString`메서드를 Overriding 해서 자주 쓰는 예 = >  DTO 
```java
public class MemberDTO {
    public String name;
    public String phone;
    public String email;
}
```
- `toString` 이 없는 경우
```
MemberDTO dto = new MemberDTO("Sangmin", " 010XXXXYYYY', "javatuning@gmail.com");
System.out.print("Name=" + dto.name + " Phone = " = dto.phone + " eMail="+ dto.email);
```
- `toString ` Overriding 한 경우
```java
public class MemberDTO {
    //중간 생략
  public String toString() {
      return "Name=" + name + "Phone= " + phone + "eMail=" + email;
  }
}
```
- 사용 경우
```java
MemberDTO = new new MemberDTO("Sangmin", "010XXXXYYYY", "java");
System.out.println(dto); // toString 자동 호출
```
- IDE에서 자동으로 생성을 도와준다.

## 객체는 == 만으로 같은지 확인 안되니, equals()를 사용.
- 기본자료형의 값 비교는 == , !=
- 참조자료형에서는 값이 아닌 주소값 비교.
- 참조자료형형 초기화시 참조자료형의 메모리에
```java
package c.inheriatnce;

public class MemberDTO {
    public String name;
    public String phone;
    public String email;
    //이하 생략
}
```
```java
package c.inheritance;

public class Equasls {
  public static void main(String[] args) {
    Equasls thisObject = new Equasls();
    thisObject.equalMethod();
  }
  
  public void equalMethod() {
      MemberDTO obj1 = new MemberDTO("Sangmin");
      MemberDTO obj2 = new MemberDTO("Sangmin");
      
      if (obj1 == obj2){
          System.out.println("obj1 and obj2 is same");
      } else {
          System.out.println("obj1 and obj2 is different");
      }
  }
}
```
```
obj1 and obj2 is different //
```
  - 두 객체는 각각의 생성자를 사용하여 만들어서 주소값이 다름.
  - 그 안에 속성값들은 name = "Sangmin", phone은 null, email도 null  로 동일하다
  - 이같은 Object 클래스에 선언되어 있는 equals() 메서드를 Overriding해 놓아야야지만 제대로 된 비교 가능
```java
public void equalMethod2() { 
    MemberDTO obj1 = new MemberDTO("Sangmin");
    MemberDTO obj2 = new MemberDTO("Sangmin");
    if(obj1.equals(obj2)){
        System.out.println("obj1 and obj2 is same");
        }else { 
        System.out.println("obj1 and obj2 is dirfferent");
        }
        }
```
```java
obj1 and obj2 is different
```
- 위 예제에서는 equals()메서드롤 비교를 하긴 했지만, 비교 대상 겍체인 MemberDTO클래스에서는 아직 equals() 메서드를 Overridng 하지 않았서 위와 같은 결과가 나온다.
- 만약 이 매서드를 Overriding  하지 않으면 equals() 메서드에서는 hashCode() 값을 비교한다.
hashCode() 값은 이미 이야기했지만, 해당 객체의 주소값을 리턴한다. 따라서 클래스의 인스턴스 변값들이 같다고 하더라도, 서로 다른 생성자로 객체를 생성했으면서 해시 코드가 다르니까 다르다는 결과가 나온 것.
  
- MemberDTO 클래스에 equals()메서드를 Overriding 하는 아래 예제
```java
package c.inheritance;

public class MemberDTO {
    public boolean equals(Object obj){
        if (this == obj) return true; // 주소가 같으므로 true
        if (obj == null) return false; // obj가 null이므로 false
        if (getClass() != obj.getClass()) return false; //클래스의 종류가 다르므로 false
        
        MemeberDTO other = (MemeberDTO) obj; // 같은 클래스이므로 형 변환 실행
      
      //이제부터는 각 인스턴스 변수가 같은지 비교하는 작업 수행
        
        if (name = null){ // name 이 null일 때
            if (other.name != null) return false; // 비교 대상의 name이 null이 아니면 false
        }else if (!name.equals(other.name)) return false; // 두 개의 email 값이 다르면 false
        
        //name과 같은 비교 수행
        if (email == null) { 
            if (other.email != null) return falas;
        }else if (!email.equals(other.email)) return false;
    if(phone == null){
        if(other.phone != null) return false;
    }else if (!phone.equals(other.phone)) return false;
    
    // 모든 과정을 거치고 false를 리턴하지 않은 객체는 같은 값을 가지는 객체로 생각해서 true를 리턴한다.
    return true;
        
  }
}
```
- 위는 IDE가 생성해준 equals() 메서드이다.
  - equals() 메서드를 Overriding할 떄에는 반드시 다음 다섯 가지의 조건을 만족시켜야한다.
    - 재귀 (reflexive) : null이 아닌 x 라는 객체의 x.equals(x) 결과는 항상 true 여야 한다.
    - 대칭(symmetric) : null이 아닌 x와 y 객체가 있을 때 y.equals(x)가 true를 리턴했다면 x.equals(y)도 반드시 true 를 리턴해야만 한다.
    - 일관(consistent) : null 이 아닌 x와 y가 있을 때 객체가 변경되지 않은 상황에서는 몇 번을 호출하더라도, x.equals(y)의 결과는 항상 true 이거나 항상 false 여야만 한다.
    - 타동적(transitive) : null이 아닌 x,y,z가 있을 때 x.equals(y)가 true를 리턴하고, y.equals(z)가 true를 리턴하면 x.equals(z)도 true를 리턴해야만 한다.
    - null과 비교 : null이 아닌 x라는 객체의 x.equals(null)의 결과는 항상 false여야 한다.
- 유의점 equals() 메서드를 Overriding 할 떄에는 hashCode()  메서드도 같이 Overriding 해야만 한다.
- 이유는 equals() 메서드를 Overriding 해서 객체가 서로 같다고 이야기 할 수 있겠지만 그 값이 같다고 해서 그 객체의 주소 값이 같지는 않기 때문이다.
- equals() 메서드의 결과가 true인데도 불구하고 hashCode() 메서드도 Object 클래스에서 제공하는 그대로를 사용하면 안된다.
- IDE에서 자동으로 생성한 MemberDTO 클래스 hashCode 메서드가 다음과 같다.

```java
package c.inheritance;

public class MemberDTO{
    // 중간생략
  public int hashCode(){
      final int prime = 31;
      int result = 1;
      result = prime * result + ((email == null) ? 0 : email.hashCode());
      result = prime * result + (((name ==null)) ? 0 : name.hashCode());
      result = prime * result + (((phone ==null)) ? 0 : phone.hashCode());
      return result;
      
  }
}
```

## 객체의 고유값을 나타내는 hashcode()
- hashCode() 메서드는 기본적으로 객체의 메모리 주소를 16진수로 리턴한다.    
만약 어떤 두 개의 객체가 서로 동일하다면, hashCode() 값은 무조건 동일해야만 한다.  
  따라서 equals() 메서드를 override하면 hashcode()메서드도 override 해서 동일한 결과가 나오도록 해야한다. (API내용)
  
- hashcode() 메서드를 구현할 때 지켜야하는 약속.
  - 자바 애플리케이션이 수행되는 동안에 어떤 객체에 대해서 이메 서드가 호출될 때에는 항상 동일한 int값을 리턴해주어야 한다. 하지만 자바를 실행할 때마다 같은 값이어야 할 필요는 전혀 없다.
  - 어떤 두개의 객체에 대하여 equlas() 메서드를 사용하여 비교한 결과가 true일 경우에, 두 객체의 hashcode() 메서드를 호출하면 동일한 int 값을 리턴해야만 한다.
  - 두 객체를 equals() 메서드를 사용하여 비교한 결과 false를 리턴했다고 해서, hashCode() 메서드를 호출한 int 값이 무조건 달라야 할 필요는 없다. 하지만 이 경우에 서로 다른 int값을 제공하면 hashtable 의 성능을 향상시키는데 도움이 된다.
  
- 위와 같은 제약 때문에 여러분들이 직접 equlas() 메서드나 hashcode() 메서드를 작성하는 것은 권장되지 않는다.