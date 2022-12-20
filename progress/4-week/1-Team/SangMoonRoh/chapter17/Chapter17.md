# 17장
## 어노테이션 이라는 것도 알아야 한다.
### 어노테이션이란? 
- 클래스나 메서드 등의 선언시에 @를 사용하는 것. (Annotation)
- Metadata라고도 불린다.
- JDK5 부터 등장했다.
#### 어노테이션 사용시
 - 컴파일러에게 정보를 알려주거나
 - 컴파일할 때와 설치 (deployment) 시의 작업을 지정하거나
 - 실행할 때 별도의 처리가 필요할 때

### 미리 정해져 있는 어노테이션은 딱 3개뿐이다.
- 자바 언어에서 사용하기 위해서 정해져 있는 어노테이션은 3개가 있다.
- 어노테이션을 선언하기 위한 메타 어노테이션이라는 것은 4개가 있다.
    - 메타 어노테이션은 선언을 위해서 존재하기 때문에 일반적으로 사용 가능한 어노테이션은 다음의 3개 뿐이다.  
      (JDK 6까지의 기준)
        - @Override
        - @Deprecated
        - @SupressWarnings
    
### @Override
- 해당 메서드가 부모 클래스에 있는 메서드를 `Override`했다는 것을 명시적으로 선언.

### @Deprecated
- 미리 만들어져 있는 클래스나 메서드가 더 이상 사용되지 않는 경우.
```
$ javac c/annotation/AnnotationSample.java
Note : c\annotation\AnnotationSample.java uses or override a deprecated API.
Note : Recompile with -Xlint : deprecation for details.
```
  - Xlint: deprecation 이라는 옵션을 추가하여 컴파일 을 다시 해서 확인해보라는 메시지가 나옴.

### @SupressWarning
- 컴파일러에서 `Warning`을 알리는 경우 " 일부러 이렇게 사용하는 것이니 경고가 필요 없다."라는 내용.

### 어노테이션을 선언하기 위한 메타 어노테이션
- 메타 어노테이션(Meta annotation)은 4개 존재
    - @Target
    - @Retention
    - @Documented
    - @Inherited
    
### @Target
- 어노티에션을 어떤 것에 적용할지를 선언할 때 사용한다.
```java
@Target(ElementType.METHOD)
```

- @Target() 괄호 안에 적용 대상을 지정하는데, 그 대상 목록은 다음과 같다.

|요소타입|대상|
|----|----|
|CONSTRUCTOR|생성자 선언시|
|FIELD|enum 상수를 포함한 필드(field)값 선언시|
|LOCAL_VARIABLE|지역 변수 선언시|
|METHOD|메서드 선언시|
|PACKAGE|패키지 선언시|
|PARAMETER|매개 변수 선언시|
|TYPE|클래스, 인터페이스, enum 등 선언시|

#### @Retention
- 얼마나 오래 어노테이션 정보가 유지되는지를 다음과 같이 선언
```java
@Retention(RetentionPolicy.RUNTIME)
```
 @Target 처럼 괄호 안에 지정하는 적용 가능한 대상은 다음과 같다.
 
| |대상|
|-----|-----|
|SOURCE|어노테이션 정보가 컴파일시 사라짐|
|CLASS|클래스 파일에 있는 어노테이션 정보가 컴파일러에 의해서 참조 가능함. <br>하지만 가상 머신(Virtual Machine)에서는 사라짐|
|RUNTIME|실행시 어노테이션 정보가 가상 머신에 의해서 참조 가능|

### @Documented
- 해당 "어노테이션에 대한 정보가 JavaDocs(API) 문서에 포함 된다는 것"을 선언.

### @Inherited
- 모든 자식 클래스에서 부모 클래스의 어노테이션을 사용 가능하다는 것을 선언.

### @interface
- 어노테이션을 선언할 때 사용하는 어노테이션

### 어노테이션을 선언해 보자
```java
package c.annotation;

//java.lang.annotation 패키지에 선언되어 있다.
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target; 
/*
 * @Target은 해당 어노테이션 사용 대상을 지정.
 * 여기서는 ElementType.METHOD를 소괄호 안에 넣어줌으로써 
 * 이 어노테이션은 매서드에 사용할 수 있다고 지정된 것.
 * */
@Target(ElementType.METHOD) //1
/*
 * @Retention 은 어노테이션 유지 정보를 지정하는 데 사용.
 * 소괄호 안에 @RetentionPolicy.RUNTIME으로 지정함녀 실행시에 이 어노태이션을 참조한다.
 * */
@Retention(RetentionPolicy.RUNTIME) //2
/*
 * 어노테이션 이름인 UserAnnotation 앞에는 @interface가 선언되어 있다. 
 * 처음 보면 익숙하지 않겠지만.
 * 클래스나 인터페이스를 선언할 때 처럼 @interface로 선언하면 @UserAnnotation 으로 어노테이션이 사용 가능해진다.
 * */
public @interface UserAnnotation { //3
    /*
     * 이노테이션 선언 안에는 number() 라는 메서드와 text() 라는 메서드가 있다.
     * number()의 리턴 타입은 int이며, text()의 리턴 타입은 String 이다. 
     * 이렇게 메서드처럼 어노테이션 안에 선언해 놓으면, 이 어노테이션을 사용할 때 해당 항목에 대한 타입으로 값을 지정 가능하다.
     * */
    public int number(); //4
    /*
     * text()를 보면 `default`라는 예약어를 쓰느 뒤 문자열이 지정되어 있는 것을 볼 수 있다.
     * default 예약어를 사용할 경우에는, default 뒤에 있는 값이 이 어노테이션을 사용할 때의 기본값이 된다. 
     * 값을 지정하지 않아도 default 값으로 지정된다.
     * */
    public String text() default "This is first annotation"; //5
}
```
- 실사용 예시
```java
package c.annotation;

public class UserAnnotationSample {
    @UserAnnotation(number = 0)
    public static void main(String[] args) {
        UserAnnotationSample sample = new UserAnnotationSample();
    }
    
    @UserAnnotation(number = 1)
    public void annotationSample1(){
    }

    @UserAnnotation(number = 2, text = "second")
    public void annotationSample2(){
        
    }

    @UserAnnotation(number = 3, text="third")
    public void annotationSample3(){
        
    }
}
```
- 두 개 이상의 어노테이션을 선언할 때에는 중괄호를 한 후 쉼표(,)로 구분해 주면 된다.
- 만약 클래스 선언시와 메서드 선언시에 어노테이션을 사용할 수 있도록 하려면
```java
@Target({ElementType.METHOD, ElementType.TYPE})
```

### 어노테이션에 선언한 값은 어떻게 확인하지?
```java
package c.annotation;

import java.lang.reflect.Method;

public class UserAnnotationCheck {
    public static void main(String[] args) {
        UserAnnotationCheck sample = new UserAnnotationCheck();
        sample.checkAnnotations(UserAnnotationSample.class);
    }
    
    public void checkAnnotations(Class useClass){
        /*
         * Class 클래스에 선언되어 있는 getDeclaredMethods() 메서드를 호출하면,
         * 해당 클래스에 선언되어 있는 메서드들의 목록을 배열로 리턴한다.
         * */
        Method[] methods = useClass.getDeclareMethods(); //1
        for(Method tempMethod : methods){
            UserAnnotation annotation = 
                    /*
                     * Method 클래스에 선언되어 있는 getAnnotation() 이라는 메서드를 호출하면,
                     * 해당 메서드에 선언되어 있는 매개 변수로 넘겨준 어노테이션이 있는지 확인하고,
                     * 있을 경우 그 어노테이션의 객체를 리턴한다.
                     * */
                    tempMethod.getAnnotation (userAnnotation.class);//2
            if (annotation!=null){
                /*
                 * 어노테이션에 선언된 메서드를 호출하면, 그 값을 리턴한다.
                 * */
                int number = annotation.number(); //3
                String text = annotation.text(); //3
                System.out.println(tempMethod.getName()
                +"() : number = " + number + "text = " + text);
            } else {
                System.out.println(tempMethod.getName()
                +"() : annoation is null.");
            }
        }
    }
}
```
```
main () : number = 0 text = This is first annotation
annotationSample1() : number=1 text=This is first annotation
annotationSample2() : number=2 text=second
annotationSample3() : number=3 text=thrid
```

### 어노테이션도 상속이 안된다.
- extends 사용 불가 ( enum도 상속 불가 하듯이)

#### 어노테이션의 용도에 따라 분류
- 제약사항 등을 선언하기 위해 : @Deprecated, @Override, @NotNull
- 용도를 나타내기 위해 : @Entity, @TestCase, @WebService
- 행위를 나타내기 위해 : @Statefull, @Transaction
- 처리를 나타내기 위해 : @Column, @XmlElement

- 어노테이션이 만들어지기 전까지 모든 자바 어플리케이션의 설정을 XML이나 `properties`라는 파일에 지정해 왔다.
  (설정이 복잡해지고, 어떤 설정이 어디에 쓰이는지 이해하려면 많은 시간이 소요되었다. )
  
#### 간단한 롬복 예시
```java
private boolean employed = true;
```
- 이 변수에 접근하기 위해서는
```java
private boolean employed = true;

public boolean isEmployed(){
    return employed;
        }
        
public void setEmployed(final boolean employed){
    this.employed = employed;
        }
```

- 롬복의 경우
```java
@Getter @Setter private boolean employed = true;
```