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
      System.out.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         
  }
} 
```