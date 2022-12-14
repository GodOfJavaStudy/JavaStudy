# 13장

## 인터페이스와 추상 클래스, enum

### 메서드 내용이 없는 interface

- 자바에서 .class 파일을 만들 수 잇는 것에는 클래스만 있는 것이 아님.
    - interface(이하 인터페이스) 와 abstract 클래스라는 것이 있다.
- 어떠 시스템을 개발하던 방법론을 사용하여 개발 한다. 그를 설명하고 공동의 절차를 만들기도 하는데 아래와 같다.
    - 분석
    - 설계
    - 개발 및 테스트
    - 시스템 릴리즈

### 분석

- 시세틈을 분석하는 단계에서 시스템을 만들어 달라고 한 사람들 (SI에서는 고객, SM에서는 현업, 고객이 별도로 없는 회사에서는 기획이 그 업무를 수행) 어떻게 개발하기를 원하는지 물어본다.
- 일련의 과정을 요구사항 분석이라고 한다.

### 설계

- 설계 단게에서는 분석 단계에서 만든 대략적은 그림을 프로그램으로 만들 수 있도록 설계하는 작업을 수행한다.
- 이 단계에서는 어떤 메서드를 만들 것인지, 데이터는 어떻게 저장할지 등등의 세부적인 것들을 정리한다.

### 개발 및 테스트

- 설계에서 만들기로 한 것들을 개발하는 단계다. 실제 시스템에서 제공해야 하는 기능들을 이 때 만든다. 이 만드는 작업을 개발이라고 한다.
- 필요한 기능들이 제대로 동작하는지 확인하는 "테스트 " 작업을 수행한다.

### 시스템 릴리즈

- 시스템을 드디어 사용자들에게 제공하는 단계.
- 프로그램은 사람이 만들기에 완벽할 수 없다 시스템을 오픈한 이후에 운영/유지보수 단계를 거치면서 문제가 있는 부분을 고쳐나간다.
- 설계 단계에서 인터페이스를 만들어두면 개발할 떄 메서드의 이름을 어떻게 할지, 매개 변수를 어떻게 할지를 일일이 고민하지 않아도 된다.
- 인터페이스나 abstract 클래스를 사용하는 이유
    - 예를 들어 전원버튼 같은 경우 누군가 가르쳐 주지 않았지만, 버튼을 누르면 전원이 켜지거나 꺼진다는 것을 알 수 있다.
    - 다음과 같이 인터페이스에 다음과 같은 메서드가 선언된 경우<br>
      ` public boolean equals(Obejct o);`<br>
      누가 봐도 메서드가 매배 변수로 넘어온 객체와 현재 객체가 같은지를 boolean으로 리턴해주는 역할을 한다고 생각할 것이다.
    - 인터페이스가 구현된 클래스가 어떻게 되어 있는지의 여부이다. 노트북 pc tv의 전원 버튼을 누르면 어떤 원리에 의해서 켜지고 꺼지는지 알 수가 없다.<bR>
      인터페이스의 역할은 이와 같다. 위의 equals() 메서드의 경우는 내가 equals() 메서드에 객체를 하나 던져줄테니 같으면 true, 다르면 false를 리턴해줘라고 이야기하는 것과 같다.<br>
      해당 메서드를 사용하는 사용자의 입장에서는 내부 구현은 궁금하지 않고, 원하는 메서드를 호출하고 그 답을 받으면 된다.
    - 가장 일반적인 것이 DAO(Data Access Object)라는 패턴이다. 이 패턴은 데이터를 저장하는 저장소에서 원하는 값을 요청하고 응답을 받는다. 여럭종류의 DBMS 가 있다.

> DBMS 는 Database Management System 의 약자로 데이터를 저장하는 저장소의 하나이며, Oracle, MYSQL , MSSQL 등의 관계형 DB(Relational Database)와 요즘 유행하는 MongoDB,CouchDB 등과 같이 NOsQl도 포함되는 포괄적 단어다.

- 인터페이스와 abstract 클래스를 사용하는 이유
    - 설계시 선언해 두면 개발할 때 기능을 구현하는 데에만 집중할 수 있다.
    - 개발자의 역략에 따른 메서드의 이름과 매개 변수 선언의 격차를 줄일 수 있다.
    - 공통적인 인터페이스와 abstract 클래스를 선언해 놓으면, 선언과 구현을 구분할 수 있다.

### 인터페이스를 직접 만들어보자

- MemberDTO를 관리하는 MemeberManagerImpl 이라는 클래스를 만들어야 한다.
- 실제 코드는 만들지 않더라도 어떤 메서드들이 있어야 하는지를 정의하려고 할 때 인터페이스를 사용하면 된다.
- `MemberManager` 라는 이름으로 만들었다. -`c.service` 이므로 c폴더 하위에 `service`폴더를 만들고 이 인터페이스 파일을 추가하면 된다.

```java
package c.service;

import c.model.MemberDTO;

public interface MemberManager {
    public boolean addMember(MemberDTO member);

    public boolean removeMember(String name, Strign phone);

    public boolean updateManager(MemberDTO member);
}
```

MemberDTO 는 c.model 패키지에 복사해 두었다.

- 중요한 점 인터페이스 선언부는 `public class`로 시작하지 않고, `public interface`로 시작.
- `interface` 내부에 선언된 메서드들은 몸통 `body`이 있으면 안 된다.
- `메서드 선언 이후에 중괄호를 열고, 닫거나, 중괄호 안에 한 줄의 코드도 있으면 안 된다.  
  그냥 중괄호는 인터페이스 선언을 위한 가장 상위의 중괄호만 있어야 한다고 생각하면 된다.
- 인터페이스 파일 이름은 어떻게 해야하나?
    - 동일하게 확장자를 .java 파일로 만들면 된다.
    - 이 파일을 컴파일 하는 방법은 일반 클래스와 동일하다.

```
C:\godofjavaj>javac c/service/MemberManager.java

C:\goodofjava>dir c\service\
  C 드라이브의 볼륨 : SSD MAIN
  볼륨 일련 번호 : 8087-DEB3
  
  C:\godofjava\c\service 디렉터리
  
20XX-0X-27 오전 09:03   <DIR>         .
20XX-0X-27 오전 09:03   <DIR>         ..
20XX-0X-27 오전 09:00                 254 MemberManager.java 
20XX-0X-27 오전 09:04                 269 MemberManager.class
              2개 파일                       523 바이트
              2개 디렉터리         6,076,309,504 바이트 남음
C:\godofjava> 
```

- 컴파일을 하고 나면 동일한 이름에 확장자가 .class 인 클래스 파일이 만들어진다.
- 소스 파일 이름과 클래스 팡리 이름만 보면 이 파일에 있는 것이 인터페이스인지 클래스인지 알 수가 없어서  
  프로젝트마다 표준을 잡는다, 보통은 명시적인 단어를 지정하지 않거나 클래스 이름 앞에 I를 붙여서 IMemberManager라고 할 수도 있다.

### 인터페이스 활용 방법

- MemberManagerImpl 이라는 클래스

```java
package c.service;

public class MemberManagerImple implements MemberManager {

}
```

- 클래스 선언문에 `implements` 라는 단어 뒤에 `MemberManager`라고 만든 인터페이스를 추가.
- 인텊에시르르 적용한다고 할 때에는 클래스 선언문에서 클래스 이름 뒤에 `implements`라는 예약어의 사전적인 의미는 "구현하다."이다. 자바의 예약어 중에서 가장 긴 단어이다.  (끝에 s가 붙는 것은
  클래스 자체가 3인칭 단수이므로.)
- 인터페이스를 구현하는 것은 상속이 아니므로 여러 개를 implements 할 수 있다.
- 인터페이스를 컴파일 하면?

```
$ javac c/service/MemberManagerImpl.java
c\service\MemberManagerImpl.java:3: error: MemberManagerImpl is not abstract and does not override abstract method updateMember(MemberDTO) in MemberManager
public class MemberManagerImple implements MemberManager {
         ^
1error
```

- MemberManagerImpl 클래스는 abstract 클래스도 아니고, MemberManager에 정의되어 있는 updateMember()라는 abstrace 메서드도 구현하지 않았다. 라는 오류.

> 참고 도대체 abstract 이 뭐길래 그런 게 아니라고 할까 ? abstract 의 사전적 의미는 "추상적인" 이라는 말이다. 자바에서는 메서드가 구현되지 않은, 인터페이스에 있는 메서드 선언문들과 같이 몸통이 없이 선언한 것을 abstract 이라는 용어로 표현한다. 다음 절의 abstract 클래스에 대한 설명을 보면 보다 잘 이해 될 것이다.

- 인터페이스를 구현할 경우 (implements 뒤에 인터페이스 이름을 나열한 경우 )에는 반드시 인터페이스에 정의된 메서드들의 몸통을 만들어 주어야만 한다.
- 메서드들을 구현해야만 한다. `MemberMnagerImpl` 클래스는 적어도 다음과 같이 구현해야만 한다.

```java
package c.service;

import c.model.MemberDTO;

public class MemberManagerImpl implements MemberManager {
    @Override
    public boolea addMember(MemberDTO member) {
        return false;
    }

    @Override
    public boolean removeMenber(String name, String phone) {
        return false;
    }

    @Override
    public boolean updateMember(MemberDTO member) {
        return false;
    }
}
```

- MemberManager 에 정의된 메서드들을 모두 구현해야만 컴파일 정상적으로 수행된다.
- 바로 이 작업이 개발 프로세스 중에서 "개발"에 해당한다.
- @Override 17장에서 배우는 어노테이션이라는 것 중 하나이다.
- 우선 명시적으로 Override 했다는 것을 알려주는 표현이라는 정도만 알고 가자.
- 설계 단계에서 인터페이스만 만들어 놓고, 개발 단계에서 실제 작업을 수행하는 메서드를 만들면 설계 단계의 산출물과 개발 단계의 산출물이 보다 효율적으로 관리된다.
- 이렇게 설계에서만 사용하려고 인터페이스를 만드는 것은 아니다. 인터페이스의 또 다른 용도는 외부에 노출되는 것을 정의해 놓고자 할 때 사용된다. <br>
  MemberManagerImpl 이라는 클래스가 있는데, 이 클래스가 "저한테 직접 이야기하지 마시구요, 공싱적인 것은 저의 대변인을 통해서 말씀하세요."라고 내 놓는 대변인이 바로 인터페이스이다.

- 인터페이스에는 지금까지 설명한 대로 구현이 되어 있는 코드가 없다.
- .class 의 확장자를 가진다고 해서 인터페이스를 그대로 사용할 수는 없다.
    - 생성자도 없고, 메서드를 내용 중 아무것도 체워져 있지 않기 때문이다.
    - InterfaceExample 클래스를 만든다.

```java
package c;

import c.service.MemberManager;

public class InterfaceExample {
    public static void main(String[] args) {
        MemberManager member = new MemberManager();
    }
} 
```

InterfaceExample 클래스는 c라는 패키지이므로 c.service 에 있는 MemberManager를 import 해야만 한다.

```java
import c.service;
```

이제 InterfaceExample 클래스를 컴파일해 보자.

```
$javc c\InterfaceExample.java
c\InterfaceExample.java:8: error: MemberManager is abstract; cannot be instantiated
MemberManger member = new MemberManager();
                              ^
1 error
```

- 에러가 발생하고 MemberManager 가 abstract 이기 때문에 초기회가 되지 않는다는 메시지가 출력된다.
- 아무것도 구현해 놓지 않고 왜 초기화하려는 것이냐.
  `main ()` 메서드의 member 객체 선언 문장을 다음과 같이 변경하자.
  (이렇게 변경하고 제대로 컴파일하기 위해서는 MemberManagerImpl 을 import 해야한다.)
  겉으로 보기에 member의 타입은 MemberManger 이다. 그리고 MemberManagerImpl 클래스에는 인터페이스에 선언되어 있는 모든 메서드들이 구현되어 있다. 실제 member의 타입은
  MemberManager 가 되기 때문에, `member`에 선언된 메서드들을 실행하면 MemberManagerImpl 에 있는 메서드들이 실행된다.

### 일부 완성되어 있는 abstract 클래스

- 인터페이스도 아닌, 클래스라고도 하기 힘든 abstract 클래스에 대해서 알아보자.
- `abstract` 사진적으로 추상적인의 의미다.
- `abstract` 클래스를 구현해 놓은 클래스로 초기화 및 실행이 가능하다.
- `MemberManagerAbstract` 라는 abstract 클래스를 보면서 더 자세히 알아보자, 필자가 만들어 놓은 MemberManagerAbstract 클래스의 소스를 보기를 전에 앞 절에서
  살펴본 `MemberManager`의 소스를 먼저 보자.

```java
package c.service;

import c.model.MemberDTO;

public interface MemberManager {
    public boolean addMember(MemberDTO member);

    public boolean removeMember(String name, String phone);

    public boolean updateMember(MemberDTO member);
}
```

- 인터페이스는 선언시 class 라는 예약어를 사용하지 않고 바로 interface 라는 예약어를 사용한다.
- 각 메서드 선언문은 일반 메서드 선언문과 동일하지만, 메서드의 몸통이 없다. 이제 abstract 클래스의 예제를 보자.

```java
package c.service;

public abstract class MemberMangerAbstract {
    public abstract boolean addMember(MemberDTO memberDTO);

    public abstract boolean removeMember(String name, String phone);

    public abstract boolean updateMember(MemberDTO member);

    public void printLog(String data) {
        Syetem.out.println("Data=" + data);
    }
}
```

- abstract 클새는 선언시 `class`라는 예약어 앞에 `abstact`이라는 예약어를 사용한 것을 볼수 있다.
- 몸통이 없는 메서드 선언문에는 abstract 라는 예약어를 명시한 것을 볼 수 있다.
- abstract 클래스는 abstract 로 선언한 메서드가 하나라도 있을 때 선언한다.
- 인터페이스와 달리 구현되어 있는 메서드가 있어도 상관 없다.
- 인터페이스와 마찬가지로 파일의 확장자는 `.java`로 하면 된다.

    - abstract 클래스는 클래스 선언시 abstract 라는 예약어가 클래스 앞에 추가되면 된다.
    - abstract 클래스 안에는 abstract 로 선언된 메서드가 0개 이상 있으면 된다.
    - abstract로 선언된 메서드가 하나라도 있으면, 그 클래스는 반드시 abstract 로 선언되어야만 한다.
    - abstract 클래스는 몸통이 있는 메서드가 0개 이상 있어도 전혀 상관 없으며 `static`이나 `final`은메스더가 있어도 된다.  
      (인터페이스는 static이나 final메서드가 선언되어 있으면 안된다.)

- abstract는 implement가 아닌 extends로 구현한다.

```java
package c.service;

import c.model.MemberDTO;

public class MemberManagerImpl2 extends MemberManagerAbstract {
}
```

- 이대로 컴파일시 에러

```
error: MemberManagerImpl2 is not abstract and does not override abstract method updateMember(MemberDTO) in MemberManagerAbstract
public class MemberManagerImpl2 extends MEmberManagerAbstract {
        ^
1error
```

- abstract로 선언되어 있는 메서드들을 구현하지 않았기 때문이다.
- 자바에서 인터페이스나 abstract 클래스의 상속을 받으면 구현되지 않은 메서드들을 구현해야한다.

```java
package c.service;

import c.model.MemberDTO;

public class MembermanagerImpl2 extends memberManagerAbstract {
    public boolean addMember(MemberDTO memberDTO) {
        return false;
    }

    public boolean removeMember(String name, String phone) {
        return false;
    }

    public boolean updateMember(MemberDTO memberDTO) {
        return false;
    }
}
```

- abstract 를 사용하는 이유
    - 인터페이스를 선언하다보니 어떤 메서드는 미리 만들어 놓아도 전혀 문제가 없는 경우 발생하는데 해당 클래스를 만들기는 좀 애매한 경우  
      아주 공통적인 기능을 미리 구현해 놓으면 많은 도움이 되는데 그것이 abstract 클래스이다.

#### 인터페이스 / 추상 클래스 / 클래스 차이 표

| |인터페이스 | abstract 클래스 | 클래스|
|---------|-------|-----|-----------|
|선언 시 사용하는 예약어|interface|abstract class | class|
|구현 안 된 메서드 포함 가능 여부 | 가능(필수)| 가능 |  불가|
|구현된 메서드 포함 가능 여부 | 불가 | 가능 | 가능 <br>( 필수 )|
|static 메서드 선언 가능 여부 | 불가|가능 | 가능 |
|final 메서드 선언 가능 여부  | 불가 | 가능 | 가능 |
|상속 (extends) 가능 | 불가 | 가능 | 가능 |
|구현(implements) 가능 | 가능 | 불가 | 불가 |

### 나는 아랫대에게 안물려줄거야

- final
    - final 은 클래스, 메서드, 변수에 선언할 수 있다.

- 클래스에 final 선언시

```java
package c.util;

public class finalClass {

}
```

- FinalClass의 객체를 생성하고 선언된 메서드를 사용하는 것은 전혀 상관 없다.
- 클래스에 final 선언시 상속을 해 줄 수 없다.

```java
package c.util;

public class FinalChildClass extends FinalClass {

}
```

- 컴파일 결과

```
error: cannot inherit from final FinalClass
public class FinalChildCalss extends FinalClass {
                                      ^
1 error 
```

- final인 FinalClass에서 상속을 받을 수 는 없다는 메시지

#### 클래스에 final 선언 이유

- 예로 String 이라는 클래스는 자바에서는 아주 중요한 클래스이고 변경을 허용 하지 않는다.  
  이러한 String 클래스 상속을 받아서 toString() 메서드에서 무조건 1을 리턴하면 String 이라는 클래스에 앧한 기본 속성을 변경을 하는 것이다.
    - <b>더 이상 확장해서는 안 되는 클래스</b>
    - <b>상속을 받아서 내용을 변경해서는 안되는 클래스를 선언할 때 final로 클래스를 선언한다.</b>

#### 메서드를 final로 선언하는 이유

- 메서드도 클래스와 비슷한 이유로 사용한다.
- 메서드를 final 로 선언하면 더 이상 Overriding 할 수 없다. 다음과 같이 FinalMethodClass 클래스에 printLog(); 메서드를 만들어 final을 선언하는 예

```java
package c.util;

public abstract class FinalMethodClass {
    public final void printLog(String data) {
        System.out.println("Data=" + data);
    }
}
```

- printLog() 메서드를 Overriding 해보면

```java
package c.util;

public class FinalMethodChildClass extends FinalMethodClass {
    public void printLog(String data) {
        System.out.println("Data = " + data);
    }
}
```

```
FinalMethodChildClass.java
error: printLog(String) in FinalMethodChildClass cannot override printLog(String) in FinalMethodClass
  public void printLog(String data){
              ^
  overridden method is final
1 error
```

- 에러 메시지를 살펴보면 "FinalMethodChildClass" 클래스에 있는 pringLog() 메서드는 final 이기 때문에 override 할 수 없다.
- 메서드를 누가 변경 하지 못하도록 final을 선언하여 다른 개발자가 그 메서드를 덮어 쓰는 것을 간단하게 막을 수 있음.

### 변수에서의 final은 메서드나 클래스에서 쓰는 것과 많이 다르다.

- 클래스나 메서드에 final을 사용하면 더 이상 상속을 못 받게 되어 Override를 할 수 없게 된다.
- 변수에 final을 사용하면 " 더 이상 바꿀 수 없다는 뜻"
- 인스턴스 변수나 static으로 선언된 클래스 변수는 선언과 함께 값을 지정해야만 한다.

```java
package c.util;

public class FinalVariable {
    final int instanceVariable;
}
```

```
c/util/FinalVariable.java
error: variable instanceVariable not initialized in the default constructor
  final int instanceVariable;
            ^
 1 error
```

- instanceVariable 은 final 로 선언되어 있어서 이렇게 선언하면 안되고 아래와 같이 해야한다.

```java
package c.util;

public class FinalVariable {
    final int instanceVariable = 1;
}
```

- 변수 생성과 동시에 초기화를 해야만 컴파일시 에러가 발생하지 않는다.
- "생성자나 메서드에서 초기화하면 되지 않나?" 라는 생각을 할 수 있지만 그러면 중복되어 변수값이 선언될 수 도 있기 때문 final의 기본 의도를 벗어난다. 이렇게 초기화를 하려면 그냥 지역 변수를 선언해서
  사용하면 된다.
- 인스턴스 변수나 클래스 변수는 생성과 동시에 초기화를 해야 된다는 것을 잊지 말자.
- 매개 변수나 지역 변수는 어떨까 ? 다음의 메서드를 FinalVariable 클래스에 추가 하자.

```java
package c.util;

public class FinalVariable {
    final int instanceVariable = 1;

    public void method(final int parameter) {
        final int localVariable;
    }
}
```

- 매개 변수나 지역 변수를 final로 선언하는 경우에는 반드시 선언할 때 초기화할 필요는 없다.
- 왜냐하면, 매개 변수는 이미 초기화가 되어서 넘어 왔고, 지역 변수는 메서드를 선언하는 중괄호 내에서만 참조되므로 다른 곳에서 변경할 일이 없다. 따라서 컴파일은 전혀 문제 없이 된다.

```java
package c.impl;

public class FinalVariable {
    //중간 생략
    public void method(final int parameter) {
        final int localVariable;
        localVariable = 2;
        localVariable = 3;
        parameter = 4;
    }
}
```

- localVariable 을 2로 선언할 때는 아무런 문제가 없다.
- 다음 줄에서 3으로 다시 선언 했다.
- 사용하면 컴파일할 때 에러가 발생한다.
- parameter는 매개 변수로 넘어오기 전에 이미 값을 정해 놓았고 final로 선언되어 있기 때문에 다시 값을 할당하면 안 된다.
- 마지막 줄처럼 사용하면 컴파일 에러가 발생한다.
    - "변하는 수" 인데, 왜 이러한 final이라는 예약어를 붙여서 값을 변경하지 못하게 만드는 걸까?
        - 어떠한 상황이 발생하지 않는 이상 내용이 변하지 않는 값을 누구나 가져다가 사용할 수 있게 .
        - final이라는 예약어를 남발해서는 안된다.

#### 지금까지는 기본 자료형에 대한 final 선언만 알아보았으니 참조 자료형도 동일하게 적용 될까?

- FinalReferenceType 클래스를 만들어보자

```java
package c.util;

import c.model.MemberDTO;

public class FinalReferenceType {
    final MemberDTO dto = new MemberDTO();

    public static void main(String[] args) {
        FinalReferenceType referenceType = new FinalReferenceType();
        referenceType.checkDTO();
    }

    public void checkDTO() {
        System.out.println(dto);
        dto = new MemberDTO();
    }
}
```

- 앞에서 사용한 MemberDTO 타입의 dto라는 변수를 final로 선언했다.
- 마찬가지로 dto도 인스턴스 변수이기 때문에 final로 선언함과 동시에 초기화를 해야만 한다.
- 그리고 나서 checkDTO() 메서드에서는 dto를 출력하고, 마지막 라인에서는 dto 객체를 다시 생성했다. 객체를 final로 선언했을 때에는 좀 다르게 처리하지 않을까?


- 이 FinalClass를 저장한 후 컴파일

```
c/util/FinalReferenceType.java
error: cannot assign a value to final variable dto
  dto = new MemberDTO();
  ^
  1 error
```

- dto 가 final 이기 때문에 값을 할당할 수 없다는 메시지와 함께 에러가 발생했다.
- 기본 자료형과 마찬가지로 참조 자료형도 두 번 이상 값을 할당하거나 새로 생성자를 사용하여 초기화할 수 없다.
- checkDTO() 메서드를 수정

```java
package c.util;

import c.model.MemberDTO;

public class FinalReferenceType {
    final MemberDTO dto = new MemberDTO();

    public static void main(String[] args) {
        FinalReferenceType referenceType = new FinalReferenceType();
        referneceType.checkDTO();
    }

    public void checkDTO() {
        System.out.println(dto);
        // dto = new MemberDTO();
        dto.name = "Sangmin";
        System.out.println(dto);
    }
}
```

```
Name = null Phone = null Email = null
Name = Sangmin Phone = null Email = null
```

- dto 객체, 즉 MemberDTO 클래스의 객체는 FinalReferenceType에서 두 번 이상 생성할 수 없다.
- 그 객체의 안에 있는 개체들은 final로 선언된 것이 아니기 때문에 그러한 제약이 없다.
- 왜냐하면 MemberDTO에서 선언되어 있는 name, phone, emial 모두 final이 아니기 때문이다.
- 해당 클래스가 final이라고 해서, 그 안에 있는 인스턴스 변수나 클래스 변수가 final이 아니다.

### enum 클래스 라는 상수의 집합도 있다.

- final로 String 과 같은 문자열이나 숫자들을 나타내는 기본 자료형의 값을 고정할 수 있다. = > 상수(constant)
- 어떤 클래스가 상수만으로 만들어져 있을 경우에는 반드시 class로 선언할 필요는 없다.
- 이럴 때 class라고 선언하는 부분에 enum이라고 선언하면 " 이 객체는 상수의 집합이다"라는 것을 명시적을 나타냄.
- enum은 enumeration 이라는 셈, 계산, 열거, 목록, 일람표 라는 영어 단어의 앞부분만 따서 만들어진 예약어이다.
- 먼저 enum 클래스는 어떻게 보면 타입이지만 클래스의 일종이다. / 열거형 클래스

```java
package c.enums;

public enum OverTimeValues {
    THREE_HOUR,
    FIVE_HOUR,
    WEEKEND_FOUR_HOUR,
    WEEKEND_EIGHT_HOUR;
}
/*
 * 어떤 회사의 평일 3시간 이상~5시간 미만일 때 야근 수당
 * 주말 4시간 이상 ~ 8시간 미만일 때의 휴일 근무 수당
 * 8시간 이상일 때의 야근 수당이 있다고 하자.
 * OverTimeValues라는 enum 클래스는 이와 같은 상황을 선언해둔것이다.
 * 이 4개의 상수에 관련된 값을 할당할 수도 있으나, 먼저 이렇게 선언만 한 경우를 살펴보자.
 * enum 클래스에 있는 상수들은 지금까지 살펴본 변수들과 다르게 별도로 타입을 지정할 필요도, 값을 지정할 필요도 없다.
 * 그냥 해당 상수들의 이름만 콤마로 구분하여 나열해 주면 된다.
 * enum 클래스에 이와 같이 상수들만 선언하면 가장 마지막 에 있는 세키몰론도 필요 없다.
 * 이 enum 클래스인 OverTimeValues 파일의 확장자도 java다. 인터페이스, abstract 클래스, enum 클래스 모두 소스 파일의 확장자는 java이며 컴파일한 파일의 확장자도 모두 .class이다.
 */
```

### 그렇다면 이러한 enum클래스는 어떻게 사용할까?

#### 가장 효과적으로 enum 클래스를 사용하는 방법은 switch문에서 사용하는 것이다.

- 다음과 같이 OverTImeManager라는 클래스를 만들고, getOverTimeAmount() 라는 메서드에서 야근 수당을 확인하여 제공하는 예제.

```java
package c.enums;

public class OverTimeManager {
    public int getOverTimeAmount(OverTimeValues value) {
        int amount = 0;
        System.out.println(value);
        switch (value) {
            case THREE_HOUR:
                amount = 18000;
                break;
            case FIVE_HOUR:
                amount = 30000;
                break;
            case WEEKEND_FOUR_HOUR:
                amount = 40000;
                break;
            case WEEKEND_EIGHT_HOUR:
                amount = 60000;
                break;
        }
        return amount;
    }
}
```

- getOverTimeAmount() 메서드를 보면 OverTimeValues 라는 enum 타입을 매개 변수로 받는다. 변수명은 values 이다.
- 야근 수당을 리턴할 amount 라는 int타입을 선언하고 0을 기본값으로 선언하고, 가장 마지막 줄에 그 값을 리턴한다.
- 메서드의 중간에는 switch문을 사용하였으며 , switch 조건으로 value를 지정하였다.
- switch 내의 case에는 OPverTimeValues에 선언한 상수 값들로 분기하도록 했다.
- 그러면 OverTimeValues 라는 enum 타입을 어떻게 getOverTimeAmount () 메서드에 전달할까,

```java
public static void main(String[]args){
        int myAmount=manager.getOverTimeAmount(OverTimeValues.THREE_HOUR);
        System.out.println(myAmount);
        }
```

- 밑에서 두 번째 줄을 보면, 별도의 생성자도 필요 없고, 그냥 enum을 넘겨주는 것이 아니라는 것을 알수 있다.
- OVerTimeValues.THREE_HOUR 를 매개 변수로 넘겨 주었다.
- enum 타입은 "enum 클래스이름.상수이름"을 지정함으로써 클래스의 객체 생성이 완료된다.

```java
int myAmount=manager.getOverTImeAmount(OverTimeValues.THREE_HOUR);
```

```java
OverTimeValues value=OverTimeValues.THREE_HOUR;
        int myAmount=manager.getOverTimeAmount(value);
```

- 여기서 value라는 변수는 OverTimeValues라는 enum 클래스의 객체라고 생각하면 된다. enum 클래스는 생성자를 만들 수 있지만, 생성자를 통하여 객체를 생성할 수는 없다. main() 메서드를
  OverTimeManager에 추가하고, 컴파일한 후에 실행한 결과는 다음과 같다.

```java
THREE_HOUR
        18000
```

- 매개 변수로 넘긴 enum 값이 THREE_HOUR로 출력된 것을 볼 수 있다.
- 출력한 결과가 이렇게 나온다고 해서 `THREE_HOUR` 라는 문자열 String 값을 getOverTimeAmount() 라는 메서드에 매개 변수로 넘기면 컴파일도 안 된다.
- 그냥 출력한 값이 저렇게 나올 뿐이라는 것을 꼭 기억해 두기 바란다.
- getOverTimeAmount () 메서드의 결과는 당연히 평일 3시간 근무일 경우 18000이므로, 정상적인 결과가 출력된 것을 볼 수 있다.

### enum을 보다 제대로 사용하기

- 그냥 enum 타입을 넘겨서 항상 switch로 확인해야할까? 그냥 enum 클래스 선언시 각 상수의 값을 지정할 수 없을까?
- 당연히 enum 상수 값을 지정하는 것은 가능하다. 단 값을 동적으로 할당하는 것은 불가능하다.

```java
package c.enums;

public enum OverTimeValues2 {
    THREE_HOUR(18000),
    FIVE_HOUR(30000),
    WEEKEND_FOUR_HOUR(40000),
    WEEKEND_EIGHT_HOUR(60000);
    public final int amount;

    OverTimeValues2(int amount) {
        this.amount = amount;
    }

    public int getAmount() {
        return amount;
    }
}
```

- enum 클래스도 생성자를 사용할 수 는 있지만, 생성자의 선언부를 보면 public이라고 되어 있지 않다.
- 이렇게 enum 클래스의 생성자는 아무것도 명시하지 않는 package-private 과 private만 접근 제어자로 사용할 수 있다.
- 그런데 public이나 protected를 생성자로 사용해서는 안된다.다시 말해서 각 상수를 enum 클래스 내에서 선언할 때에만 이 생성자를 사용할 수 있다.
- 그렇다면 앞절에서 사용한 enum 클래스는 생성자도 없는데 어떻게 이상없이 작동했을까?
- enum클래스는 일반 클래스와 마찬가지로 컴파일 할때 생성자를 자동으로 만들어준다.

```java
package c.enums;

public class OverTimeManager2 {
  public static void main(String[] args) {
    OverTimeValues2 values2 = OverTimeValues2.FIVE_HOUR;
    System.out.println(values2);
    System.out.println(values2.getAmount());
  }
}
```

- value2라는 변수에 OverTimeValues2 의 FIVE_HOUR라는 상수를 할당해 놓았다.
두 번째 줄에서는 value2를 출력하였고, 마지막 줄에선느 value2의 getAmount()라는 메서드를 호출하였다.
```
FIVE_HOUR
30000
```

### enum 클래스의 부모는 무조건 java.lang.Enum 이어야 한다.
- 자바에서는 다중 상속은 허용되지 않지만, 일반 클래스들은 상속에 상속을 거쳐 여러 부모 클래스들을 가질 수 있다.
- enum 클래스는 무조건 java.lang.Enum 이라는 클래스의 상속을 받는다.
- enum을 선언하여 사용할때 마음대로 extends하면 안 된다.
- 누가 만들어 놓은 enum을 extends를 이용하여 선언할 수는 없다.
- Enum 이라는 모든 enum 클래스의 부모가 어떻게 되어 있는지 살펴보자.
   - Enum 클래스의 생성자는 다음과 같이 선언되어 있다.

|접근 제어자 | 메서드 | 설명|
|----------|-------|----|
|protected|Enum(String name, int ordinal) | 컴파일러에서 자동으로 호출되도록 해놓은 생성자다. 하지만 개발자가 이 생성자를 호출 할수는 없다.|
- name 은 enum 상수의 이름
- ordinal은 enum의 순서 / 상수가 선언된 순서대로 0부터 증가한다.
- Enum 클래스의 부모 클래스는 object 클래스이기 때문에, Object 클래스의 메서드들은 모두 사용할 수 있다.  
하지만  Enum클래스는 개발자들이 Object 클래스 중 4개의 메서드를 Overriding 하지 못하도록 막아놓았다.
  
|메서드|내용|
|-----|------|
|clone()|객체를 복제하기 위한 메서드이다. 하지만 이 메서드는 enum 클래스에서 사용하면 안된다.<br> 만약 호출될 경우엔 ConeNotSupportedException이라는 예외를 발생 시키도록 되어 있다.|
|finalize()|GC가 발생할 때 처리하기 위한 메서드이다.|
|hashCode()|int 타입의 해시 코드 값을 리턴하는 메서드다.|
|equals()|두 개의 객체가 동일한지를 확인하는 메서드다.|

- hashCode() , equals() 메서드는 사용해도 무방하다. 그중에섣 equals()메서드를 가장 많이 사용한다.  
clone()과 finalize() 메서드는 사용하면 안된다.
  
- Object 클래스의 메서드를 Overriding 한 마지막 메서드는 toString() 메서드다.  
기본적으로 enum 변수에 이 메서드를 호출하면 앞에서도 본 것처럼 상수 이름을 출력한다.  
  toString() 메서드는 Enum 클래스에서 Overridinggks object 클래스의 메서드 중에서 유일하게 final로 선언되어 있지 않다.
#### Enum 클래스 안에 선언되어 있는 메서드   
|메서드 | 내용 |
|------|-----|
|compareTo(E e) | 매개 변수로 enum 타입과의 순서(ordinal) 차이를 리턴한다.|
|getDeclaringClass() | 클래스 타입의 enum을 리턴한다|
|name() | 상수의 이름을 리턴한다|
|ordinal()| 상수의 순서를 리턴한다|
|valueOf(Class<T> enumType, String name) | static 메서드다. 첫 번째 매개 변수로는 클래스 타입의 enum을 두 번째 매개 변수로는 상소의 이름을 넘겨주면 된다.

- compareTo() 메서드는 이 순서가 같은지 다른지를 비교하는 데 사용 된다. 만약 같은 상수라면 0을 그렇지 않고 다르면 순서의 차이를 출력한다. <bR>
순서의 차이는 메서드의 매개 변수로 넘기는 상수 기준으로 앞에 있으면 음수(-) 뒤에 있으면 양수(+)를 리턴한다 .
```java
package c.enums;

public class OverTimeManager2{
  public static void main(String[] args) {
    OverTimeValue2 overTimeValue2 = OverTimeValues2.FIVE_HOUR;
    System.out.println(value2.compareTo(value2));
  }
}
```
```
FIVE_HOUR
30000
1
```
- 매개 변수로 넘긴 THREE_HOUR는 FIVE_HOUR앞에 선언되어 있따. 그러므로 FIVE_HOUR, THREE_HOUR 는 FIVE_HOUR 바로 앞에 선언되어 있다, FIVE_HOUR 는 THEREE 하나 뒤에 있으니 1을 결과로 출력한다.
- enum  클래스에 values()는 모든 상수를 배열로 리턴한다.

```java
package c.enums;
public class OverTimeManager3 {
  public static void main(String[] args) {
    OverTimeValue2 []valueList= OverTimeValues2.value();
    for (OverTImeVaules2 value :valueList) {
        System.out.println(value);     
    }
  }
}
```
