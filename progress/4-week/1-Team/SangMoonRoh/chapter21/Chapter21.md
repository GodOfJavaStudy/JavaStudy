# 21장
## 실수를 방지하기 위한 제네릭이라는 것도 있어요.

### 실수를 방지할 수 있도록 도와주는 제네릭

> `private` 변수, `getter`, `setter`, `Serializable` 구현을 해야만 제대로 된 DTO 클래스이다.

```java
package d.generic;

import java.io.Serializable;

public class CastingDTO implements Serializable {
    private Object object;

    public void setObject(Object object) {
        this.object = object;
    }

    public Object getObject() {
        return object;
    }
}
```

```java
package d.generic;

public class GenericSample {

    public static void main(String[] args) {
        GenericSample sample = new GenericSample();
        sample.checkCastingDTO();
    }
    
    public void checkCastingDTO() {
        CastinDTO dto1 = new CastingDTO();
        dto1.setObject(new String());

        CastinDTO dto2 = new CastingDTO();
        dto2.setObject(new StringBuffer());

        CastinDTO dto3 = new CastingDTO();
        dto3.setObject(new StrinBuilder());
    }
} 
```

- 위 코드에서 Object 클래스는 모든 클래스의 부모 클래스이므로 매개변수로 어떤 참조 자료형이 오더라도 상관이 없다.  
하지만 값을 꺼낼 때 문제가 발생된다. 각 개체의 getObject() 메소드를 호출했을 때 리턴값으로 넘어오는 타입은 Object이다.  
그래서 다음과 같이 `String`,`StringBuffer`, `StringBuilder`타입으로 각각 형 변환을 해야한다.
```java
String temp = (String) dto1.getObject();
StringBuffer temp2 = (StringBuffer)dto2.getObject();
StringBuilder temp3 = (StringBuilder)dto3.getObject();
```
- 혼동될 경우 `instanceof`를 사용하여 변환을 확인 후 진행할 수 있다.
- 이러한 혼동을 막기 위해 제네릭이 자바5부터 추가되었다.
### 제네릭이 뭐지?
- 제네릭은 실행시에 예외가 발생하는 것을 처리하는 것이 아니라, 컴파일 할 때 점검할 수 있도록 한 것을 말한다.

```java
package d.generic;

import java.io.Serializable;

public class CastingDTO implements Serializable {
    private Object object;

    public void setObject(Object object) {
        this.object = object;
    }

    public Object getObject() {
        return object;
    }
}
```

- 제네릭을 사용한다면 ?

```java
package d.generic;

import java.io.Serializable;

public class CastingGenericDTO<T> implements Serializable {
    private T object;

    public void setObject(T obj) {
        this.object = obj;
    }

    public T getObject() {
        return object;
    }
}
```

- `T`는 아무런 이름이나 지정해도 컴파일하는 데에 전혀 상관 없다.

```java
package d.generic;

import java.io.Serializable;

public class CastingGenericDTO<godOfJava> implements Serializable {
    private godOfJava object;

    public void setObject(godOfJava obj) {
        this.object = obj;
    }

    public godOfJava getObject() {
        return object;
    }
}
```
- 이처럼 꺾쇠 안에는 현재 존재하는 클래스를 사용해도 되고, 존재하지 않는 것을 사용해도 된다.
  - 되도록이면 클래스 이름의 명명 규칙과 동일하게 지정하는 것이 좋다.
  - 꺽쇠 안에 선언한 그 이름은 클래스 안에서 하나의 타입 이름처럼 사용하면 된다,
  - 만약 타입 이름이 존재하는 클래스여야 한다면 컴파일시에 에러가 발생한다.
  - 꺾쇠 안에 있는 그 이름은 가상의 타입 이름이라고 생각하면 된다.

```java
package d.generic;

public class GenericSample {
    public static void main(String[] args) {
        GenericSample sample = new GenericSample();
        sample.checkGenericDTO();
    }
    public void checkGenericDTO(){
    
        CastingGenericDTO<String> dto1 = new CastingGenericDTO<String>();
        dto.setObject(new String());
        CastingGenericDTO<StringBuffer> dto2 = new CastingGenericDTO<StringBuffer>();
        dto2.setObject(new StringBuffer());
        CastingGenericDTO<StringBuilder> dto3 = new CastingGenericDTO<StringBuilder>();
        dto3.setObject(new StringBuilder());
    }
}
```

- 명시적으로 타입을 지정할 때 사용하는 것이 제네릭이다. 

### 제네릭 타입의 이름 정하기
- E : 요소 (Element, 자바 컬렉션에서 주로 사용됨)
- K : 키
- N : 숫자
- T : 타입
- V : 값
- S,U,V : 두 번째, 세 번째, 네 번째에 선언된 타입

### 제네릭에 ? 가 있는 것은 뭐야?
- 제네릭을 사용할 때 <> 안에 들어가는 타입은 기본적으로 어떤 타입이라도 상관 없다.

```java
package d.generic;

public class WildcardGeneric<W> {
    W wildcard;
    public void setWildcard(W wildcard) {
        this.wildcard = wildcard;
    }
    
    public W getWildcard() {
        return wildcard;
    }
}
```

```java
package d.generic;

public class WildcardSample{

    public static void main(String[] args) {
        WildcardSample sample = new WildcardSample();
        sample.callWildcardMethod();
    }
    
    public void callWildcardMethod(){
        WildcardGeneric<String> wildcard = new WildcardGeneric<String>(); // callWildcardMethod() 메서드에서는 방금 만든 WindcardGeneric이라는 클래스에 String을 사용하는 제네릭한 객체를 생성한다.
        wildcard.setWildcard("A");
        wildcardStringMethod(wildcard); //생성한 객체로 wildcardStringMethod()를 호출할 때 넘겨준다.
    }
    
    /*
     * wildcardStringMethod() 에서는 해당 매개 변수를 받아서 결과를 출력한다.
     * */
    public void wildcardStringMethod(WildcardGeneric<String> c ){
        String value = c.getWildcard();
        System.out.println(value);
    }
}
```

- 만약 다른 타입으로 선언된 WildcardGeneric 객체를 받으려면 어떻게 해야할까? 
    - WildcardGeneric<Integer> 와 같이 선언된 객체를 받는 경우를 이야기 하는 것이다.
    - 지금까지의 방법으로는 답이 없다.  
  제네릭한 클래스의 타입만 바꾼다고 `Overloading`이 불가능하기 때문이다.

```java
public void wildcardStringMethod(WildcardGeneric<?> c){
    Object value = c.getWildcard();
    System.out.println(value);
        }
```

- String 대신에 ? 를 적어주면 어떤 타입이 제네릭 타입이 되더라도 상관없다.  
하지만 메서드 내부에서는 해당 타입을 정확히 모르기 때문에 앞서 사용한 것처럼 `String` 으로 값을 받을수 없고, `Object`로 처리해야만 한다.
- ? 를 wildCard 타입이라고 부른다.

- 만약 넘어오는 타입이 두세 가지로 정해져 있다면, `instanceof` 예약어를 사용하여 해당 타입을 확인하면 된다.
```java
public void wildcardStringMethod(WildcardGeneric<?> c){
    Object value = c.getWildcard();
    if(value instanceof String){
        System.out.println(value);
        }
        }
```

- wildcard는 메서드의 매개 변수로만 사용하는 것이 좋다.  
`wildcardStringMethod()`를 호출한 `callWildcardMethod()`에서 만약 다음과 같이 사용한다면 

```java
public void callWildcardMethod(){
    WildcardGeneric<?> wildcard = new WildcardGeneric<String>();
    wildcard.setWildcard("A");
    wildcardStringMethod(wildcard);
        }
```

- 컴파일 되지 않음.
- 알 수 없는 타입에 String을 지정할 수 없다는 말이다.
  - 어떤 객체를 wildcard로 선언하고, 그 객체의 값은 가져올 수는 있지만, 와일드 카드로 객체를 선언했을 때에는 이 예제와 같이 특정 타입으로 값을 지정하는 것은 "불가능"하다.

### 제네릭 선언에 사용하는 타입의 범위도 지정 가능하다.
- wildCard로 사용하는 타입을 제한할 수 있다.
- ? 대신에 `? extends 타입`으로 선택하는 것이다.

```java
package d.generic;

public class Car {
    protected String name;
    public Car(String name){
        this.name = name;
    }
    
    public String toString(){
        return "Car name =" + name;
    }
}
```

```java
package d.generic;

public class Bus extends Car {
    public Bus (String name){
        super(name);
    }
    public String toString(){
        return "Bus name = " + name;
    }
}
```

-  ? 라는 wildcard는 어떤 타입이 오더라도 상관이 없었다.
  - ? 대신 `? extends Car`라고 적으면 제네릭 타입으로 Car를 상속받은 모든 클래스를 사용할 수 있다는 뜻이다.
  - 따라서 매개 변수에는 다른 타입을 제네릭 타입으로 선언한 객체가 넘어올 수 없다.  
    - 컴파일시에 에러가 발생하므로 반드시 Car 클래스와 관련되어 있는 상속한 클래스가 넘어와야만 한다.
- `? extends 타입` 과 같은 것을 `Bounded Wildcards`라고 부른다.
  - Bound 라는 말은 경계라는 의미도 있기 때문에, 매개 변수로 넘어오는 제네릭 타입의 경계를 지정하는 데 사용한다는 의미로 해석하면 된다.
- ? 로 사용하는 wildcard와 마찬가지로 여러분들이 Bounded Wildcards로 선언한 타입에는 값을 할당할 수 없는 없다. 
    - 이와 같이 조회용 매개 변수로 사용해야만 한다.

### 메서드를 제네릭하게 선언하기
- `wildcard`로 메서드를 선언하는 방법에는 단점이 있다. 
  - 매개 변수로 사용된 객체에 값을 추가할 수가 없다. 
- 아래와 같은 방법이 있긴 하다.

```java
package d.generic;

public class GenericWildcardSample {
    public static void main(String[] args) {
        GenericWildcardSample sample = new GenericWildcardSample();
    }
    
    public <T> void genericMethod(wildcardGeneric<T> c, T addValue){
        c.setWildcard(addValue);
        T value = c.getWildcard();
        System.out.println(value);
    }
}
```
- 메서드 선언부를 잘 보면 리턴 타입 앞에 <> 로 제네릭 타입을 선언해 놓았다.
  - 매개 변수에서는 그 제네릭 타입이 포함된 객체를 받아서 처리한 것을 볼 수 있다.
  - 매서드의 첫 문장을 보면 `setWildcard()`메서드를 통하여 값을 할당까지했다.

- `?`를 사용하는 Wildcard 처럼 타입을 두리뭉실하게 하는 것보다는 이처럼 명시적으로  메서드를 선언시 타입을 지정해주면 보다 견고한 코드를 작성할 수 있다.
  - Bounded Wildcards 처럼 사용하는 방법은
`public <T extends Car> void boundedGenericMethod(WildcardGeneric<T> c, T addValue)`
  - 내가 만들 메서드는 이러한 제네릭 탕비이 두 개인데, 이럴 떈 어떻게 하지? 
    - 한 개 이상의 제네릭 타입 선언은 콤마로 구분하여 나열하여 주면 된다.
```java
public <S,T extends Car> void multiGenericMethod(WildcardGeneric<T> c, T addValue, S another)
```
-  이렇게 하면 S와 T 라는 제네릭 타입을 메서드에서 사용할 수 있다.