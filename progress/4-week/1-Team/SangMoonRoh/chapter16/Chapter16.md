# 16장

## 클래스 안에 클래스가 들어갈 수도 있구나

### 클래스 안의 클래스

- 자바 안에서는 클래스 안에 클래스`Nested`클래스가 들어갈 수 있다.
- 사용의 큰 이유는 코드를 간단하게 표현하기 위함이다.
- Nested 클래스는 자바 기반의 UI처리를 할 떄 사용자의 입력, 외부의 이벤트에 대한 처리를 하는 곳에서 가장 많이 사용된다.
- Nested 클래스는 선언한 방법에 따라 `Static nested` 클래스와 내부(`innerClass`)로 구분된다.
    - `Static nested` 클래스와 내부 클래스의 차이는 `Static`으로 선언되었는지 여부다.
    - 내부 클래스는 내부/로컬 클래스`inner Class`와 "익명 내부 클래스" anonymous inner class라고 부른다.

|Nested Class|||
|----|----|----|
| |Static nested Class||
| |inner Class||
| | |Local inner class|
| | |Anonymous inner Class|

- Nested 클래스를 만드는 이유
    - 한 곳에서만 사용되는 클래스를 논리적으로 묶어서 처리할 필요가 있을 때
    - 캡슐화가 필요할 때 (예를 들어 A라는 클래스에 private 변수가 있다. 이 변수에 접근하고 싶은 B라는 클래스를 선언하고, B 클래스를 외부에 노출시키고 싶지 않을 경우가 여기에 속한다.)<br>
    - 소스의 가독성과 유지보수성을 높이고 싶을 때

### Static nested 클래스의 특징

- 내부 클래스는 감싸고 있는 외부 클래스의 어떤 변수도 접근할 수 있다. (private 포함)
- Static nested 클래스를 그렇게 사용하는 것은 불가능하다. ( Static 하기 때문이다.)

```java
package c.inner;

public class OuterOfStatic { // OuterOfStatic 이라는 클래스를 선언
    static class StaticNested { //
        private int value = 0;

        private int getValue() {
            return value;
        }

        public void setValue(int value) {
            this.value = value;
        }
    }
}
```

```
OuterOfStatic.class
OuterOfStatic$StaticNested.class
```

- Static nested 클래스는 $ 기호를 붙인 후 Nested 클래스의 이름이 나온다.

```java
package c.inner;

public class NestedSample {

    public static void main(String[] args) {
        NestedSample sample = new NestedSample();
        sample.makeStaticNestedObject();
    }

    public void makeStaticNestedObject() {
        OuterOfStatic.staticNested staticNested = new OuterOfStatic.staticNested();
        staticNested.setValue(3);
        System.out.println(staticNested.getValue);
    }
}
```

- Static Nested 클래스를 만들었을 때 객체 생성은 클래스 파일 이름처럼 중간에 $을 쓰는 것이 아니라, 감싸고 있는 외부 클래스 이름 뒤에 . 을 찍고 쓰면 된다.

### 내부 클래스와 익명 클래스

- Static이 없는 Inner 클래스의 객체를 생성하는 방법도 다르다.

```java
package c.inner;

public class OuterOfInner {
    class Inner {
        private int value = 0;

        public int getValue() {
            return value;
        }

        public void setValue(int value) {
            this.value = value;
        }
    }
}
```

```java
package c.inner;

public class InnerSample {
    public static void main(String[] args) {
        InnerSample sample = new InnerSample();
        sample.makeInnerObject();
    }

    public void makeInnerObject() {
        OuterOfInner outer = new OuterOfInner(); // 외부에서 감싸는 클래스를 먼저 생성
        OuterOfInner.Inner inner = outer.new Inner(); // 외부에 감싸는 클래스의 객체를 이용하여 Inner클래스 객체 생성
        inner.setValue(3);
        System.out.println(inner.getValue());
    }
}
```

- 익명 클래스를 생성하는 예제

```java
package c.inner;

public class MagicButton {
    public MagicButton() {

    }

    private EventListener listener;

    public void setListener(EventListener listener) {
        this.listener = listener;
    }

    public void onClickProcess() {
        if (listener != null) {
            listener.onClick();
        }
    }
}
```

- 사용하는 EventListener

```java
package c.inner;

public interface EventListener {

    public void onCLick();
}
```

```java
package c.inner;

public class AnonymousSample {
    public static void main(String[] args) {
        AnonymousSample sample = new AnonymousSample();
        sample.setButtonListener();
    }

    public void setButtonListener() {
        MagicButton button = new MagicButton();
        button.setListener(   /*   Param    */);
        button.onClickProcess();
    }
}
```

```java
package c.inner;

public class AnonymousSample {
    public static void main(String[] args) {
        AnonymousSample sample = new AnonymousSample();
        sample.setButtonListener();
    }

    public void setButtonListener() {
        MagicButton button = new MagicButton();
        button.setListener(   /*   Param    */);
        button.onClickProcess();
    }

    class MagicButtonListener implements EventListener {
        public void onClick() {
            System.out.println("Magic Button Clicked!!! ");
        }
    }
}
```

```java
package c.inner;

public class AnonymousSample {
    public static void main(String[] args) {
        AnonymousSample sample = new AnonymousSample();
        sample.setButtonListener();
    }

    public void setButtonListener() {
        MagicButton button = new MagicButton();
        MagicButtonListener listener = new MagicButtonListener();
        button.setListener(listener);
        button.onClickProcess();
    }

    class MagicButtonListener implements EventListener { // inner Class
        public void onClick() {
            System.out.println("Magic Button Clicked!!! ");
        }
    }
}
```

```java
package c.inner;

public class AnonymousSample {
    public static void main(String[] args) {
        AnonymousSample sample = new AnonymousSample();
        sample.setButtonListener();
    }

    public void setButtonListener() {
        MagicButton button = new MagicButton();
        MagicButtonListener listener = new MagicButtonListener();
        button.setListener(new EventListener() { // Anonymous Class  익명 클래스
            public void onClick() {
                System.out.println("Magic Button Clicked!!! ");
            }
        });
        button.onClickProcess();
    }
}
```

- 익명 클래스나 내부 클래스는 모두 다른 클래스에서 재사용할 일이 없을 때 만들어야한다.
- 어느 정도 익숙해지면, 오히려 익명 클래스를 사용함으로써 코드의 가독성이 높아질 수도 있지만, 그 반대의 경우도 생길 수 있기 때문에 너무 남용하지는 말 것.

### Nested 클래스의 특징

```java
package c.inner;

public class NestedValueReference {
    public int publicInt = 0;
    protected int protectedInt = 1;
    int justInt = 2;
    private int privateInt = 3;
    static int staticInt = 4;

    static class StaticNested {
        public void setValue() {
            staticInt = 14; // static 외의 변수 참조 불가
        }
    }

    class Inner { // private 등등 모든 변수 참조가능
        public void setValue() {
            publicInt = 20;
            protectedInt = 21;
            justint = 22;
            privateInt = 23;
            staticInt = 24;
        }
    }

    public void setValue() {
        EventListener listener = new EventListener() { // private 등등 모든 변수 참조가능
            public void onClick() {
                publicInt = 30;
                protectedInt = 31;
                justInt = 32;
                privateInt = 33;
                staticInt = 34;
            }
        };
    }
}
```

- 반대로 참조 가능
```java
package c.inner;

public class ReferenceAtNested {
    static class StaticNested {
        private int staticNestedInt = 99;
    }
    class Inner {
        private int innerValue = 100;
    }
    
    public void setValue(int Value){
        StaticNested nested = new StaticNested();
        nested.staticNestedInt = value;
        Inner inner = new Inner();
        inner.innerValue = value;
    }
}
```