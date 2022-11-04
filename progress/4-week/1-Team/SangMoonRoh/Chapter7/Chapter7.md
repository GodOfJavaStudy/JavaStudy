# 여러 데이터를 하나에 넣을 수는 없나요 ?
- 배열 : 가장 일반적인 자료 구조
> 자료 구조는 데이터를 저장하기 위한 구조.  
> 가장 대표적인 자료 구조 : List , Queue, Map, LinkedList
- 배열은 한 가지 타입에 대해서, 하나의 변수에 여러 개의 데이터를 넣을 수 있다. 
  - 기본 자료형의 배열 선언
    - ```java
      int[] lottoNumbers;
      int lottoNumbers[];
      ```
- 대괄호를 사용하여 배열이라는 것을 정의함.
- 배열 변수를 정의할 때 대괄호 안에는 아무것도 써주면 안된다.
- 대괄호는 타입과 변수 사이, 변수명 뒤에 위치해도 된다. ( 보ㅓ통은 첫번째 있는 것과 같이 타입과 변수명 사이에 대괄호를 넣는 것을 권장.)
- 위와 같이 선언한 배열은 몇개의 데이터가 들어가는지 알 수가 없다. 따라서
  - ```java
    int [] lottoNumbers = new int[7]'
    ```
- 배열의 값을 지정하는 법 
  - ```java
    lottoNumbers[1] = 15; // 배열의 두번째 자리에 15라는 값을 지정.
    ```
    
- 배열에서의 수의 시작 크기가 7 이라면 index는 0~6까지다. 0 으로부터 시작
> main() 메서드에도 args라는 배열을 매개 변수로 받고 있다.

- index의 크기 이상으로 초기화, 참조 등을 하면 `Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 7` 과 같은 예외 발생한다
### 배열의 기본 값
- 기본 자료형 배열의 기본 값은 각 자료형의 기본 값과 동일하다.
- 배열에서는 지역 변수라도 배열의 크기만 정해주면 문제가 발생하진 않는다.
- 굳이 배열의 크기를 크게 잡을 필요 없이 1로만 지정하면 배열의 기본 값이 할당된다.
- char 배열의 기본 값은 `\u0000'이다.
- 모든 참조 자료형의 초기화 작업이 없었다면 null 이다.
- 초기화한 인덱스는 결과가 출력되고 그렇지 않다면 null이다.
> 왜 ArrayInitValue 객체를 출력한 결과는 타입의 이름과 함께 이상한 골뱅이 (@)가 붙은 암호 같은 것이 출력되어 있는 것일까?
> 참조 자료형은 public String toString() 이라는 메소드를 만들어 줘야만 이러한 암호 같은 내용이 출력되지 않는다.
- 모든 배열은 참조 자료형.
- String배열의 값으로 확인해보면
  -`[Ljava.lang.String;@1540e19d] 
  - [L: 가장 앞의 [는해당 객체가 배열이라는 의미.다음 L은 해당 배열은 참졸 자료형이라는 의마.
  - java.lang.String : 해당 배열이 어떤 타입의 배열인지를 보여준다.
  - @1540e19d 해당 배열의 고유 번호다.
  - byte 는 [B
  - short 는 [S
  - int는 [I
  - float [f
  - double [D
  - char [C
  - long의 배열과 boolean 의 배열만이 각각 J와 Z로 이미 기존에 예약어가 있어서 지정되어있다.

### 배열을 선언하는 또 다른 방법
```java
public class ArrayInitialize {
  public static void main(String[] args) {
    ArrayInitialize array = new ArrayInitialize();
    int [] lottoNumber = {5,12,23,25,38,41,2};
    
    int[] lottoNumbers2;
    lottoNumbers2 = {5,12,23,25,38}; //컴파일 에러
  }
}
```
- 보통은 절대 변경되지않을 값을 지정할때 중괄호로 선언하여 사용 ( 아래 예시)
```java
public class ArrayInitialize {
  public static void main(String[] args) {
    ArrayInitialize array = new ArrayInitialize();
    System.out.println(array.getMonth(3));
    //중간 생략
  }
    public String getMonth( int monthInt ){
        String [] month = {"january","February","March","April","May","June","July","August","September","October","November","December"};
        return month[monthInt+1];
    }
  
}
```
- 그런데 보통은 이 예에서 사용한 달 처럼 변하지 않는 값은 메소드 내에서 선언하여 사용하는 것보다는 클래스의 변수로 선언하여 재활용하는 것이 좋다.
```java
public class ArrayInitialize {
        String [] month = {"january","February","March","April","May","June","July","August","September","October","November","December"};
}
```
- 만약 getMonth()라는 메소드에서만 이 month라는 배열을 사용한다면 반드시 메소드 밖으로 빼낼 필요는 없다.
- ArrayInitialize라느 클래스의 객체를 생성할 때마다 month라는 배열이 생성되기 때문이다.
- 얼마나 자주 사용하는지 어디에서 사용하는지를 확인하여 메서드에서 선언하여 사용할지, 클래스의 인스턴스 변수로 선언하여 사용할지 결정하면 된다.
- 이렇나 단점을 해결하기 위해서 존재하는 자바의 예약어가 있는데 바로 static이라는 에약어이다.
```java
public class ArrayInitialize {
static String [] month = {"january","February","March","April","May","June","July","August","September","October","November","December"};
}
```
- `static` 이라고 선언하면 클래스 변수가 된다.

### 별로 사용하지는 않지만, 알고 있어야 하는 2차원 배열
- 배열에는 2차원 3차원 4차원 배열도 만들 수 있다.
- 2차원 배열의 예제
```java
public class ArrayTwoDimension {
  public static void main(String[] args) {
    ArrayTwoDimension array = new ArrayTwoDimension();
    array.twoDimensionArray();
  }
  public void twoDimensionArray(){
      int [][] twoDim;
      twoDim = new int [2][3]; // 혹은 int [] twoDim[]; int twoDim[][];
  }
}
```
- 1차원 배열처럼 타입과 배열 변수명 사이에 대괄호들을 넣는 것을 권장한다고 함.
- 2차월 배열은 "배열의 배열"을 의미한다.
- 2차월 배열 `twoDim[][]`에서 `twoDim[0] = int 배열`, `twonDim[0][0] = int 값` ==> 중요
- `twoDimensionArray()` 메서드에서처럼 한번에 1차원과 2차원의 크기를 지정할 수 있다.
  - 보통 2차원 배열에서 앞에 있는 대괄호를 1차원, 뒤에 있는 대괄호를 2차원이라고 이야기한다.
  
|twoDim[0][0]|twoDim[0][1]|twoDim[0][2]|
|------------|------------|------------|
|twoDim[1][0]|twoDim[1][1]|twoDim[1][2]|

- 2차원 배열은 `twoDim= new int[2][];`과 같이 선언할 수도 있다.
  - 1차원의 크기만 지정하고, 2차원의 크기를 지정하지 않을 수도 있다. 하지만 1차원 배열은 빈공간으로 놔두고, 2차원 배열만 지정하거나, 두 배열의 공간의 크기를 모두 지정 하지 않으면 컴파일 에러.
  - `twoDim = new int[][];` -----> X  `twoDim= new int[][2];`-----> X
  - 이 선언은 `twoDim[0]와 twoDim[1]` 두 개의 배열만 선언해 놓은 것이기 때문이다. 
  - `twoDim = new int[2][];`로 배열을 선언했을 때 `twoDim[0]` 배열의 크기는 반드시 정해줘야 한다.
  ```
  twoDim[0] = new int [3];  // 1차원 배열을 선언한 다음에는 2차원 배열을 다음과 같이 선언한다.
  twoDim[1] = new int [2];
  ```
  
- 처음 선언한 2차원 배열(twoDim= new int[2][3]) 은 1차원과 2차원의 크기가 고정되어 있었다.
- 하지만 위와 같이 따로 따로 선언한다면 배열의 공간 크기를 서로 다르게 지정할 수 있다.
- 2차원 배열의 초기화 다른 방법
`int [][]twonDim = {{1,2,3},{4,5,6}};`이다.
- 이렇게 선언하는 것은 다음과 같이 선언하는 것과 같다.
```
int [][] twoDim = new int[2][3];

twoDim [0][0] = 1;
twoDim [0][1] = 2;
twoDim [0][2] = 3;

twoDim [1][0] = 4;
twoDim [1][1] = 5;
twoDim [1][2] = 6;
```
- 이렇게 twoDim 배열이 있을 때 배열에 선언되어 있는 값을 출력하려면 어떻게 해야할까? 
  - 배열의 길이를 확인하여 for루프를 사용할 수도 있다.

### 배열의 길이 확인하기
- 배열의 이름에 .length를 붙여준다.
```java
public class ArrayLength{
  public static void main(String[] args) {
    ArrayLength array = new ArrayLength();
    array.printArrayLength();
  }
  
  public void printArrayLength(){
      int[] oneDim = new int[3];
      int[][] twoDim = new int[4][2];
      System.out.println(oneDim.length); //3
      System.out.println(twoDim.length);// 4
  }
}
```
- 2차원 배열의 경우 1차원의 크기를 알려준다. 2차원 배열의 크기를 알고 싶다면 각1차원 배열에 `.length`를 붙여야만 한다.
- 즉 `twomDim[0].length`, `twomDim[1].length`, 처럼 각 1차원 1ㅐ열의 길이를 알려달라고 해야한다.
```
int twoDim0_0Lenth = twoDim [0][0].length; // 사용 안됨 twoDim[0][0] 은 배열 객체를 나타내는 것이 아니라 값이 들어가는 공간이다.
```
- int 와 같은 기본 자료형에는 절대로 .length 와 같이 점을 찍어서 기능을 호출하거나 계산을 할 수 없다.
- 배열과 같이 차조 자료형에서만 점(.)을 찍을 수 있다.
```
public void printArray(){
int [][]twoDim = {{1,2,3},{4,5,6}};
System.out.println("twoDim.length ="+twoDim.length);
System.out.println("twoDim[0].length ="+twoDim[0].length);

for(int oneLoop=0;oneLoop < 2; oneLoop++){
  for(int twoLoop=0; twoLoop<3; twoLoop++){
  System.out.println("two DIim["+oneLoop+"]["+twoLoop+"]=}"+twoDim[oneLoop][twoLoop]);
   }
  }
 }
}
```
```
for (int oneLoop=0; oneLoop<twoDim.lenth; oneLoop++){
for (int twoLoop=0; twoLoop<twoDim[oneLoop].length;twoLoop++){
System.out.print("twoDim["+oneLoop + "]["+twoLoop+"]= " + twoDim[oneLoop][twoLoop]);
}
```
### 배열을 위한 for 루프
> jDK 부터 개선 된 부분
```
for( 타입이름 임시변수명 : 반복대상 객체){

}
```

```
public void twoDimFor(){
int [][]twoDim = {{1,2,3},{4,5,6}};
for(int[] twoDimArray: twoDim){ // int[] twoDimArray 로 지정했다 (int의 배열을 앞부분에 기재)
  for(int data:dimArra){ // 안에 있는 for루프를 보면 dimArray 배열의 1차원 값이 int타입이기때문에 때문에 int data라고 지정..
  System.out.println(data);
  }
}
```

### 자바 실행할 때 원하는 값들을 넘겨주자.
```java
public class ArrayMain{
  public static void main(String[] args) {
    
  }
}
```
- args라는 String타입 배열에는 어떻게 값을 전달할까?
```java
public class ArrayMain{
  public static void main(String[] args) {
      if (args.length > 0 ){
          for (String args:args){
              System.out.println(args);
          }
      }
    
  }
}
```
- 이렇게 해두면 args에 전달되는 데이터가 하나라도 있을때 for루프를 수행하면서 해당 값을 출력할것이다.
`ArrayMain`뒤에 a b c d를 한칸씩 띄워서 입력한 후 실행
```
java ArrayMain a b c d
a
b
c
d
$
```
- 이렇게 클래스 이름 뒤에 공백으로 분리한 문자열을 나열하면 이 문자열들이 args라는 배열에 전달된다.
- 어플리케이션이 시작할 때 전달해야하는 값들이 있다면 이와 같은 방법으로 사용된다.