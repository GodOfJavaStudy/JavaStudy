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
  
