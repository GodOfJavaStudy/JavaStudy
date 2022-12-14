#자바를 배우면 패키지와 접근 제어자는 꼭 알아야해요!
## 패키지는 그냥 폴더의 개념이 아니다.
- 자바 어플리케이션을 개발할 때 클래스들을 분류하지 않으면 이름이 중복되거나, 어떤 클래스가 어떤 일을 하는지 혼동을 막기 위해 사용하는 것.

### 패키지 선언시 제약사항
1. 소스의 가장 첫 줄에 있어야만 한다.  
만약 `package`선언 위에 주석이나 공백이 있어도 상관은 없지만, 다른 자바 문장이 하나라도 있으면 컴파일이 제대로 되지 않는다.
   
2. 패키지 선언은 소스 하나에는 하나만 있어야 한다.  
한 소스 파일이 두 개의 폴더에 한번에 존재할 수 없기 때문에 당연하다.
   
3. 패키지 이름과 위치한 폴더 이름이 같아야만 한다.  
만약 자바 파일을 만들어 놓은 폴더의 이름과 여기에 선언된 패키지의 이름이 다를 경우, `javac`로 컴파일하려고 하면 파일을 찾지 못해 컴파일이 되지 않는다.  
   따라서 패키지 이름을 정할 때에는 해당 파일이 존재하는 위치와 동일하게 패키지를 지정해야만 한다.
   
### 패키지 이름 지정시 유의점
- 패키지 이름이 `java`로 시작해서는 안됨.

### 패키지 이름을 짓는 법
- 기본 규칙

|패키지 시작 이름|내용|
|-----------|-----|
|java|자바 기본 패키지(Java 벤더에서 개발)|
|javax|자바 확장 패키지(Java 벤더에서 개발)|
|org|일반적으로 비 영리단체(오픈 소스)의 패키지|
|com|일반적으로 영리단체(회사)의 패키지|

#### 자바 패키지의 이름을 지정할 때 유의점
- 패키지 이름은 모두 소문자 지정  
반드시는 아니지만 소문자로 사용하기로 약속이 되어 있다.
  
- 자바의 예약어를 사용하면 절대 안 된다. `int`,`static`등의 단어가 패키지 이름에 들어 있으면 안 된다. (`com`,`int`,`util` 등 )
- 하위 패키지 이름을 정해야만 한다.
- 반드시 가장 상위 패키지 아레에 주요 구분되는 패키지가 존재할 필요는 없고, 개발 되는 패키지의 표준을 어떻게 정하느냐에 따라 패키지를 구분하면 된다.

#### import를 이용하여 다른 패키지에 접근하기
- 같은 패키지 안의 클래스들과 `java.lang` 패키지에 있는 클래스들만 찾을 수 있다.
- 다른 패키지에 있는 클래스를 사용하려면 `import`라는 예약어를 사용해야 한다.
```java
import 다른패키지.하위패키지.클래스명; // 단일 클래스
import 다른패키지.*; // 패키지 내부 전부지만 하위 패키지는 import 하지 않는다. (같은 레이어의 패키지만)
import static 다른패키지.하위패키지.클래스명.staticMethod;// static 한 변수(클래스 변수)와 static 메서드를 사용하고자 할 때 용이하다.
import static 다른패키지.하위패키지.클래스명.STATIC_FILED_NAME; // static 한 변수명

public class PakageStatic{
    public static void main(String[] args) {
        staticMethod();
        System.out.println(CLASS_NAME);
    }
}
```
- `import static`으로 `static`한 변수나 메서드를 지정하면 굳이 클래스 이름을 지정하지 않아도 `PacakgeStatic`클래스에 선언된 것처럼 사용할 수 있다.
#### import 하지 않아도 사용 가능한 패키지
- `java.lang` 패키지
- 같은 패키지
- 폴더 구조상 상위 패키지에 있는 클래스와 하위 패키지에 있는 클래스의 상관관계는 자바 언어상에 없다.


### 자바의 접근 제어자( Access modifier)
- public : 누구나 접근 가능
- protected : 같은 패키지 내에 있거나 상속 받은 경우
- package-private : 아무런 접근 제어자를 적어주지 않았을 경우, 같은 패키지 내에 있을 때만 접근할 수 있다.
- private : 해당 클래스 내에서만 접근 가능하다.  
  
public > protected > package-private > private 

|구분 |해당 클래스 안에서 | 같은 패키지에서 | 상속 받은 클래스에서 | import한 클래스에서|
|----|----------------|--------------|-------------------|------------------|
|public|O|O|O|O|
|protected|O|O|O|X|
|(package private)|O|O|X|X|
|private|O|X|X|X|\

### 클래스 접근 제어자 선언시 유의점
- 한 자바파일에 클래스가 두개 선언되어 있다면 클래스 파일이 두개 생성.
- 단 클래스 선언이 `package private`이기 떄문에 같은 패키지 내에 있는 클래스들만이 이 클래스의 객체를 생성하고 사용할 수 있다.
- 한 자바 파일에 두 클래스 중 두 번째 클래스가 `public`이라면, 이 클래스의 소스 파일은 `PublicSecondClass.java`여야만 한다.  
`public`으로 선언된 클래스가 소스 내에 있다면, 그 소스 파일의 이름은 `public`은 클래스 이름과 동일해야만 한다.
- `public`이 붙은 클래스 이름과 소스 파일이 동일해야함 => 파일명은 `public`이 붙은 클래스를 따라야함. 

