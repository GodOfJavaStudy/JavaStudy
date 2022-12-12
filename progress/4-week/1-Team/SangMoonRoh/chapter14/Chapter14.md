#다 배운 것 같지만, 예외라는 중요한 것이 있어요
## 자바에서 매우 중요한 예외
- 자바에는 예외 (Exception)이라는게 있다.
- "There is no rule has no exception." 예외 없는 규칙이란 없다.
  - 우리가 예상한 혹은 예상치 못한 일이 발생 하는 것을 미리 예견하고 안전장치를 하는 것
    - ex :  
    - 고객이 상품 선택 -> 상품 가격 확인 -> 카드나 현금 전달-> 계산 처리 -> 물건포장
    - 고객이 상품 선택 -> 상품 가격 획인 -> 가격 흥정 시작 -> 버티기 -> 가격 흥정 반복 후 못 이기는 척 깎아줌 -> DC율 결정 -> 카드나 현금 전달 -> 계산 처리 -> 물건 포장
- 예외적인 일이 발생하게 되면 "예외"라는 것을 던져버린다.
    - ex: NULL인 객체에 메서드를 호출 / 5개의 공간을 가지는 배열을 만들었는데 6번째 값을 읽으라고 하는 등.
    
### try-catch는 짝
```java
package c.exception;

public class ExceptionSample {
    public static void main(String[] args) {
        ExceptionSample sample = new ExceptionSample();
        sample.arrayOutOfBounds();
    }
    public void arrayOutOfBounds(){
        int[] intArray = new int[5];
        System.out.println(intArray[5]);
    }
}
```
- 정상적으로 컴파일은 되지만, 실행시에 `RunTimeException`으로  
`java.lang.ArrayIndexOutOfBoundsException:` 라는 에러가 발생한다.  
  배열의 범위 밖에 있는 위치를 요청한 예외
- 아랫줄로는 at 로 시작하는 스택 호출 추적(영어로 call stack trace)문장들이 출력된다.
- `Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException : 5`
- 이 호출 관계의 가장 윗줄에는 예외가 발생한 클래스와 메서드 이름과 줄의 반호를 출력한다.
- `at c.exception.ExceptionSample.arrayOutOfBounds(ExceptionSample.java:11)`
- 그 아래에는 그 메서드를 호출한 클래스 (c.exception.ExceptionSample)과 메서드의 이름 및 줄 번호를 출력한다.

```java
public void arrayOutOfBoundsTryCatch(){
    try{
        int[] intArray = new int[5];
        System.out.println(intArray[5]);
        }catch (Exception e){

        }
        }
```
- try 뒤에 중과호로 예외가 발생하는 모든 문장을 묶어 주고, catch 괄호 안에 예외가 발생했을때 처리
```java
public void arrayOutOfBoundsTryCatch(){
        try{
        int[] intArray = new int[5];
        System.out.println(intArray[5]);
        System.out.println("thid code should run.");
        }catch (Exception e){

        }
        }
```
- 출력결과 없음.
```java
public void arrayOutOfBoundsTryCatch(){
        try{
        int[] intArray = new int[5];
        System.out.println(intArray[5]);
        System.out.println("thid code should run.");
        }catch (Exception e){
        System.out.println("Exception occured.");
        }
        System.out.println("This code must run.");
        }
```
- catch 문 안에 System.out 이 아니라 System .err 로 다르게 넣으면 IDE에서 출력결과가 다른 색으로 표시된다.
```
Exception occured.
This code must run.
```
- try 블록 내에서 예외가 발생하면, 예외가 발생한 줄 이후에 있는 try 블록 내의 코드들은 수행되지 않음.   
  그 다음 catch 블록에 있는 문장이 실행됨.
  - try 블록 내에서 예외가 발생하지 않으면 catch 내에 있는 코드는 실행되지 않고 try-catch 구문 밖에 있는 문장이 실행된다.
  
- <b style="color:Orange">try-catch에서 예외가 발생하지 않는 경우</b>
  - try 내에 있는 모든 문장이 실행되고 try-catch 문장 이후의 내용이 실행된다.
- <b style="color:Orange">try-catch에서 예외가 발생하는 경우</b>
  - try내에서 예외가 발생한 이후의 문장들은 실행되지 않는다.
  - catch 내에 있는 문장은 반드시 실행되고, try-catch 문장 이후의 내용이 실행된다.
  
### try-catch 를 사용하면서 처음에 적응하기 힘든 변수 선언
- try-catch 안에서 공통된 변수를 사용하려면 try-catch문 이전에 변수 선언을 하여 사용해야 한다.

### finally야 ~ 넌 무슨 일이 생겨도 반드시 실행해야 해
- try-catch 구문에 붙을 수 있는 블럭 = > finally
- 자바에서 예외를 처리할 때 finally는 어떠한 경우에도 넌 반드시 실행해 라는 의미.
- finally 블럭은 예외 발생 여부와 상관 없이 실행된다.
- try-catch의 변수 할당과 마찬가지로 사용한다.

### 두 개 이상의 catch
- catch 블록이 시작되기 전에(중괄호가 시작되기 전에) 있는 소괄호에는 예외의 종류를 명시한다.  
  - 항상 Exception e라고 쓰는 것은 아니다.
  
```java
try {
    System.out.println(intArray[5]);
        } catch(ArrayIndexOutOfBounds) { 
        System.out.println("ArrayIndexOutOfBoundsException occurred");
        } catch (Exception e){
    System.out.println(intArray.length);
        }
```
- try는 한번만 쓰고,. catch블록을 여러 개 만들어도 전혀 문제 없다.
- catch 블럭은 순서를 따진다.
```
error: exception ArrayIndexOutOfBodunsException has already been caught }
catch (ArrayIndexOutOfBoundsException e){
^
1 error
```

#### Exception의 비밀에 대해서
- 모든 예외의 부모 클래스는 `java.lang.Exception` 클래스다. 
- Exception 클래스는 java.lang 패키지에 선언되어 있기 때문에 별도로 import할 필요는 없다.

- 예외는 부모 예외 클래스가 이미 catch 를 하고 자식 클래스가 그 아래에서 catch를 하도록 되어 있을 경우에는 자식 클래스가 예외를 처리할 기회가 없다.
- Exception 클래스가 모든 클래스의 부모 클래스이고 배열에 발생시키는 ArrayIndexOutOfBoundsException Exception 클래스의 자식 클래스이기 때문에 절대로 Exception 클래스로 처리한 catch 블럭 이후에 선언한 블럭은 처리될 일이 없다.
  - intArray의 5번쨰 값을 찾는 작업을 하기 전에 해당 객체가 null인지 확인하는 작벙르 먼저 할지, 아니면 그 반대일지를 생각해보자.
  - null 인 객체를 갖고 작업하면 안되기 때문에 해당 객체가 null인지 확인 하는 작업은 반드시 먼저 선행되어야 한다.
  - Exception 클래스로 catch 하는 것은 가장 아래에 추가할 것.
  
- try 다음에 오는 catch 블럭은 1개 이상 올 수 있다.
- 먼저 선언한 catch 블록의 예외 클래스가 다음에 선언한 catch 블럭의 부모에 속하면 자식에 속하는 catch 블럭은 절대 실행될 일이 없으므로 컴파일되지 않는다.
- 하나의 try 블럭에서 예외가 발생하면 그 예외와 관련이 있는 catch 블럭을 찾아서 실행한다.
- catch 블록 중 발생한 예외와 관련있는 블럭이 없으면, 예외가 발생되면서 해당 쓰레드는 끝난다.
  (이 부분에 대해서는 나중에 쓰레드를 배워야 이해가 쉽다.) 따라서 마지막 catch 블록에는 Exception 클래스로 묶어주는 버릇을 들여놓아야 안전한 프로그램이 될 수 있다.
  
### 예외의 종류는 3가지다 .
- 각 예외의 종류 
  - checked exception
  - error
  - runtime exception 혹은 unchecked exception
  
#### error
- 에러는 자바 프로그램 밖에서 발생한 예외.
  - 서버의 디스크가 고장 났거나, 메인보드 등의 문제
  - 자바 프로그램에서 오류가 발생 되었을 때 오류의 이름이 error로 끝나면 에러, Excption 으로 끝나면 예외이다.
- Error와 Exception으로 끝나는 오류의 가장 큰 차이는 프로그램 안에서 발생했는지 밖에서 발생했는지 여부이다.
  - 프로그램이 멈추어 버리느냐, 계속 실행할수 있느냐의 차이.
  - Error는 프로세스에 영향을 준다.
  - Exception은 쓰레드에만 영향을 준다 .
  
#### runtime exception(이하 런타임 예외)
- 런타임 예외는 예외가 발생할 것을 미리 감지하지 못했을 때 발생한다.
- 런타임 예외에 해당 하는 모든 예외들은 RuntimeException을 확장한 예외들이다.
  - 컴파일할 때 예외가 발생하지 않는다.
  - 실행시에는 발생할 가능성이 있다. 
  - 컴파일 시에 체크를 하지 않기 때문에 unchecked exception 이라고보 부르는 것이다.
  
  - Throwable 
    - Error<br>
    - Exception<br>
      - RunTimeException<br>
        - NPE
        - NumberFormatException
        - ClassCastException
        - IndexOutOfBoundsException
  
      - IOException
      - SQLException
      - MalformedURLException ...
  
- Excpetion 을 바로 확장한 클래스들이 Cehcked 예외이다.
- RuntimeExcpetion 밑에 확장되어 있는 클래스들이 런타임 예외들이다.

### 모든 예외의 할아버지는 java.lang.Trowable 클래스다.
- Exception과 Error의 공통 부모 클래스는 당연히 Object 그리고 java.lang.Throwable 클래스다.
- Exception 이나 Error 클래스는 Throwable 클래스를 상속받아 처리하도록 되어 있다.
- Exception 이나 Error를 처리할 때 Throwalbe로 처리해도 무관하다.

- Throwable()
- Throwable(String message)
- Throwable(String message, Throwable cause)
- Throwable(Throwable cause)

- 매개변수 없는 생성자는 기본적으로 제공.
- 예외 메세지를 String으로 넘겨줄 수도 있다.
- 별도로 예외의 원인을 Throwable 객체로 넘겨 줄수도 있다.
 - getMessage()
 - toString()
 - printStackTrace()

#### getMessage()
- 예외 메세지를 String  으로 형태로 제공 받는다.  
- 예외가 출력되었을 때 어떤 예외가 발생되었는지를 확인할 때 매우 유용하다.
  - 별도의 예외 메시지를 사용자에게 보여주려고 할 때 좋다.
    
#### toString() 
- 예외 메시지를 String형태로 제공 받는다.
- 그런데 getMessage() 메서드보다는 약간 더 자세하게 예외 클래스 이름도 같이 제공한다.

#### printStackTrace()
- 가장 첫 줄에는 예외 메시지를 출력하고, 두 번째 줄부터는 예외가 발생하게 된 메서드들의 호출 관계(스택 트레이스)를 출력해준다.
```java
} catch (Throwable t) {
    
        }
```

- catch 의 빈공 간에 다음의 한 줄을 추가한다면
`System.out.println(t.getMessage());`
  - t는 catch블럭에  선언한 Throwable 클래스의 객체 이름이다.
    

### 난 예외를 던질거니까 throws 라고 써 놓을꼐
- 자바에서는 예외를 던질 수 있다 .
- 자바에서 예외를 발생시키는 방법을 알아보자.
```java
try{ 
    if(number>12){
        throw new Exception("Number is over than 12");
        }
        }
```
- try 블록 내에서 throw 라고 명시한 후 개발자가 예외 클래스의 객체를 생성하면 된다.
- 다른 예외가 발생한 상황과 동시하게 trhow한 문장 이후에 있는 모든 try블럭 내의 문달드은 수행이 되지 않고 catch 블럭으로 이동한다. 
- catch 블럭 중에 throw한 예외와 동일하거나 상속 관계에 있는 예외가 있다면 그 블럭에서 예외를 처리할 수 있다.
- 예외가 없다면 발생된 예외는 메서드 밖으로 던져버린다.
- 예외가 발생된 메서드를 호추한 메서드로 던진다느 의미.
```java
public void throwsException(int number) throws Exception{
    if(number>12){
        throw new Exception ("Number is over than 12");
        }
    System.out.println("Number is " + number);
        }
```
- 예외 발생시 try-catch 로 묶어주지 않아도 그 메서드를 호출한 메서드로 예외 처리를 위임하는 것이기 떄문에 문제가 되지 않는다.
- try-catch 블럭으로 묶지 않아도 예외를 throw한다고 할지라도 throws 가 선언되어 있기 때문에 전혀 문제 없이 컴파일 및 실행이 가능하다.
    - throws가 선언되어 있기 때문에 전혀 문제 없이 컴파일 및 실행이 가능하다.
    - 이렇게 throws로 메서드를 호출한 메서드에서는 반드시 try-catch 블럭 throwsException()메서드를 감싸주어야 한다.그렇지 않을 경우 컴파일 에러가 발생한다. 
    
```
error: unreported exception Exception ; must be caught or declared to be thrown
                                            sample.throwsException(13);
```

- caught되거나 throw한다고 선언되어 있어야 한다 라는 메시지가 뜬다.
- throws 문장으로 인한 컴파일 오류가 생겼을 경우 두 가지 있다.
    - try -catch 사용
    - 호출한 메서드 다시 throws 하는 메서드를 합니다.
    

#### trows와 throw 정리
- 메서드를 선언할 때 매개 변수 소괄호 뒤에 throws라는 예약어를 적어준 뒤 예외를 선언하면, 해당 메서드에서 선언한 예외가 발생했을 때 호출한 메서드로 예외 전달.
-   만약 메서드에서 두가지 이상의 예외를 던질 수 있다면 implements 처럼 콤마로 구분하여 예외 클래스 이름을 적으면 된다.
- try블록 내에서 예외를 발생시킬 경우에는 throw 라는 예약어를 적어 준 뒤 예외 객체를 생성하거나 생성되어 있는 객체를 명시 해준다.
- throw한 예외 클래스가 catch 블럭에 선언 되어 있지않아서 throws선언에 포함되지 않으면 
- cathc 블럭에서 예외를 thows할 경우에도 구문에 해당 예외가 정의되어 있어야만 한다.

### 예외를 만들 수 도 있다.

[comment]: <> (- Throwablde)
