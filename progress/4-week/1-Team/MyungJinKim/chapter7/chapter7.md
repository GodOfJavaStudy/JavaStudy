##7장 여러 데이터를 하나에 넣을 수 없는 걸까요?
***

###배열
* 한 변수에 여러개의 값을 넣을 수 있는 것 (일반적인 자료구조 중 하나)
  * 자료구조란 데이터를 저장하기 위한 구조를 의미한다 (2권에서 자세히)

```java
//기본 자료형의 배열
int [] lottoNumbers;
int lottoNumbers[];
```
* 배열을 선언 할 때 대괄호를 열고 닫음으로써 해당 변수가 배열이라는 것을 정의 할 수 있다.
  * 배열 변수를 정의할 때 대괄호 안에는 아무것도 쓰면 안된다 ex) int[2] a;
* 배열을 선언 할 때 몇개의 데이터가 들어가는 지 알수 없어 초기화를 해줘야 된다

```java
int[] lottoNumber = new int[2];
```
* new int[2] 와 같이 배열을 선언 할 때 new를 써준 후 타입 이름을 명시 해준 다음 배열의 크기를 지정한다
* int는 기본자료형이지만 int[] 와 같이 int[] 배열로 만든 lottoNumbers는 참조자료형이다
* 배열도 참조 자료형이기 때문에 new를 붙여야 된다

```java

int [] lottoNumber;
lottoNumber = new int[7]; // 7개의 값을 지정 할 수 있다
lottoNumber[1] = 15; // 배열의 두번째 자리에 15값을 지정
```
* 대괄호 안에는 데이터를 넣고자 하는 위치를 지정 해 주면 된다 위치는 index라고 한다
* 배열의 위치는 0부터 시작한다

```java
public class Array {

  public void init(){
    int [] lottoNumbers = new int[7]; // 임의의 7개의 값을 저장
    lottoNumbers[0] = 6;
    lottoNumbers[1] = 0;
    lottoNumbers[2] = 1;
    lottoNumbers[3] = 2;
    lottoNumbers[4] = 3;
    lottoNumbers[5] = 4;
    lottoNumbers[6] = 5;
    lottoNumbers[7] = 7;

  }
    
    public static void main(String[] args) {
        Array array = new Array();
        
    }
}
```

```
메소드 안에 메소드를 또 쓰는 중첩메소드는 거의 없다(클래스는 중첩이 가능하다)
main메소드 안에 메소드 정의는 특별한 경우에만 된다
public static void main(String[] args) {

      Comparator<Integer> compare = new Comparator<Integer>() {

            @Override

            public int compare(Integer o1, Integer o2) {

                  return o1 - o2;

            }

      };

}

 Comparator 인터페이스가 자바 표준 라이브러리에 포함되어있기 때문에 가능한 정의입니다.

이것 외의 사용자 정의 함수를 main 메소드 내부에 정의하려고 하면, 오류가 발생합니다.

따라서 main 메소드 외부에 메소드를 정의해준 후에 main 메소드에서 사용해주시면 됩니다.

static 메소드의 경우, main 메소드에서 클래스.메소드명 으로 사용할 수 있습니다.
인스턴스 생성이 필요하지 않습니다.
그 외의 메소드의 경우, 인스턴스를 생성해준 후에 사용할 수 있습니다.
객체 생성 후 객체.메소드명 으로 사용할 수 있습니다.

https://www.inflearn.com/questions/25520
```

실행을 하면 에러가 난다
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 7
at Array.start(Array.java:13)
at Array.main(Array.java:19)

* ArrayIndexOutOfBoundsException는 array배열 index위치 OutOfBounds 벗어난 Exception 예외
  * 배열은 7개의 공간을 갖고 0~6까지의 index를 가지지만 위에서 7번째 자리에 값을 할당하려기 때문에 예외처리 된다
  * java.lang.ArrayIndexOutOfBoundsException: 7 의 7은 잘못 지정한 위치를 말한다


***

### 배열의 기본값
* 기본자료형 배열의 기본 값은 각 자료형의 기본값과 동일하다
* 지역변수의 경우에는 초기화를 하지 않으면 사용이 불가능 하지만 배열에서는 배열의 크기만 정해주면 에러가 발생하지 않는다
* 배열의 크기만 잡아주면 초기화를 하지 않아도 배열의 기본값이 할당 된다
* char배열의 기본 값은 \u0000 이며 출력 될 때 한칸의 공백으로 보인다 다른 값들은 기본 값인 0을 보여주지만 boolean의 기본 값은 false다 
* 모든 참조형은 초기화(new라는 예약어를 써서 생성자를 부르는 작업)을 하지 않으면 null 이다
   * String의 경우 new String() 과 같이 생성자를 사용하지 않고 ""만으로도 초기화를 할 수 있지만 대부분의 참조자료형은 new를 사용해서 생성자를 불러야지만 객체를 생성할 수 있다
* null은 무소유의 개념이며 아무런 값도 없고 초기화도 되어있지 않는 상태를 null이라고 부른다
  * String[] a = null 처럼  배열과 같은 참조 자료형을 선언할 때 명시적으로 무소유의 상태를 나타낼 때 이런식으로 쓸 수 있다
* 참조자료형은 public String toString()이라는 메소드를 만들어 줘야지만 내용이 출력된다
  * toString()이라는 메소드를 만들어 주지 않으면 타입이름@해시값 순으로 출력된다
* 각 배열의 크기를 지정하여 배열 객체를 초기화만 하면 기본값이 지정된다 
  * 참조자료형의 경우 초기화를 하지 않으면 null 값이 출력 된다

***
### 배열을 출력하면?
* strings = [Ljava.lang.String; @4554617c // array =[LArray;@74a14482
  *  java.lang.String 어디 위치에 있는지 패키지
  * [L : 가장 앞 [는 배열이라는 의미고 L은 해당 배열은 참조자료형이라는 의미
  * java.lang.String : 해당 배열이 어떤 타입의 배열인지 보여준다
  * @4554617c: 해당 배열의 해시값이다

```
byte=[B@1b6d3586
short=[S@4554617c
int=[I@74a14482
long=[J@1540e19d
float=[F@677327b6
double=[D@14ae5a5
char=[C@7f31245a
boolean=[Z@6d6f6e28
```
long은 L참조 자료형과 구분이 안돼서 j이고 boolean은 byte와 구분이 안돼서 z다

***

### 배열을 선언하는 방법

* 위에서는 new int[1] 과 같이 new라는 예약어를 사용하며 타입과 크기를 지정하는 것 말고 한번에 배열을 선언 할 수 있다
  * 중괄호를 써서 배열을 한번에 사용 할 수 있다
```java
public void Array{
    
    public void otherInit(){
        int[] lottoNumbers = {5,12,33,25,48,41,2};
    }

    public void otherInit2(){
        int[] lottoNumbers;
        lottoNumbers2 = {5,12,33,25,48,41,2};
    }
}

```
* 배열을 선언과 함께 초기화를 할려면 중괄호 안에 각 위치에 해당하는 값을 ,로 구분하여 나열하면 된다. 마지막 세미콜론은 필수
* otherInit2()처럼 하면 안된다 중괄호를 사용하는 배열은 선언과 초기화를 같이 해야 된다
* 위치에 맞는 값을 넣어야 되기 때문에 절대 변경되지 않는 값을 지정 할 때 중괄호를 써서 선언한다
* 자주 쓰는 배열을 사용 하게 되면 메소드 밖에 클래스의 변수로 선언하여 재활용 하는 것이 좋다
  * 해당 메소드에서만 사용하면 뺄 필요가 없다 왜냐면 Array라는 클래스의 객체를 생성 할 때마다 month라는 배열이 생성되기 때문이다
  * 얼마나 자주 사용하는지에 따라서 매서드에서 선언할지 클래스의 인스턴스로 선언하여 사용할지 결정하면 된다

```java
public void Array{

       static String[] month = {"january","February","March"};
public void otherInit(){
        int[] lottoNumbers = {5,12,33,25,48,41,2};
        }
        
        }

```
* 위처럼 static를 사용하면 객체를 생성할 때 마다 배열을 새로 생성하지 않아도 된다
* 클래스에 변수를 선언할 때 static를 선언하면 클래스 변수가 된다

***
## 2차열 배열
```java

public class Array{
    public void twoADimentsionArray(){
        int [][] twoDim;
        twoDim= new int[2][3]; // 차열 배열 선언
    }
}
```
* 2차열 배열을 나타낼 때에는 선언할 때 두개의 대괄호를 타입과 변수명 사이에 선언하면 된다 꼭 대괄호를 타입과 변수명 사이에 선언 할 필요는 없다
  * int[] twoDim[]; // int twoDim[][]
  * 1차원 배열처럼 타입과 배열 변수명 사이에 대괄호를 넣는 것을 권장한다 (보통 2차원 배열에서 앞에 있는 대괄호는 1차원 그 뒤는 2차원이라고 한다)
  * 1차원 배열은 twoDim[0]은 int값이 였지만 2차원배열은 int값이 아니라 배열이다 즉 twoDim[][]가 int값이다


* twoDim[2][3]

| twoDim[0][0] | twoDim[0][1] | twoDim[0][2] |   
|:------------:|:------------:|:------------:|
| twoDim[1][0] | twoDim[1][1] | twoDim[1][2] | 

* 세로 2개 가로 3개 / 1차원 2개의 공간 2차원 3개의 공간 이므로 2*3 = 6 의 공간을 가지게 된다
* 2차열 배열을 나타낼 때는 1차열만 크기를 지정해도 된다 
  *ex) twoDim[0][] twoDim[][]  둘다 선언이 안된다
* twoDim = new int[2][]; 을 선언했을 때 twoDim[0]배열의 크기는 반드시 정해줘야된다
  * twoDim[0] = new int [3]; twoDim[1] = new int [2];

| twoDim[0][0] | twoDim[0][1] | twoDim[0][2] |    
|:------------:|:------------:|:------------:|
| twoDim[1][0] | twoDim[1][1] |              | 

* 가로 2개 세로 3개 
* 1번째 위치에는 2차열이 2개

* 초기화 및 값을 지정할 때 int [][]twoDim ={{1,2,3},{4,5,6}}
```java
int [][] twoDim = new int[2][3];
toDim [0][0]=1;
toDim [0][1]=2;
toDim [0][2]=3;
toDim [1][0]=4;
toDim [1][1]=5;
toDim [1][2]=6;
```

###배열의 길이
* 배열의 길이는 배열의이름.length를 붙여주면 된다
```java
int [][] twoDim = {{1,2,3},{4,5,6};
System.out.println("twoDim.length = " + twoDim.length);
System.out.println("twoDim[0].length = " + twoDim[0].length);
```
* twoDim.length은 1차원의 배열의 크기가 2이기 때문에 2이고 twoDim[0].length 는 2차원의 크기가 3이기 때문이다
* 1차열의 크기를 출력할려면 대괄호 없이 .length를 쓰면 되고 2차열의 크기를 출력할려면 1차열 위치를 대괄호에 명시하면 된다
* twoDim[0][0].length 를 하면 안된다
  * 배열 객체를 나타내는 것이 아니라 값이 들어가있는 공간이기 때문이다
  * 모든 기본 자료형은 .length를 쓸 수 없다 참조자료형에서만 .를 쓸 수 있다
  * 배열을 선언 할 때는 중괄호 안에 if나 while이 들어갈 수 없다 배열의 타입에 맞는 타입만 들어갈 수 있다.
  
***

```java
// 향상된 for문
for(타입이름 임시변수명: 반복되는 대상 객체){
}
```
* 배열의 0번째 위치부터 마지막 ㅟ치까지 값이 순서대로 for를 돌면서 할당된다 
```java
for(int[] tempArray:twoDim){ -->1
        for(int temp:tempArray){ -->2
        }
}

```
* 1번째는 twoDim 이라는 배열의 1차원 값은 배열이다 그래서 int tempArray가 아니라 int[] tempArray이다
* 2번째는 for 루프를 보면 tempArray의 배열이 1차원 값이 int 타입이여서 int temp로 지정한 것이다
* 배열의 값만을 처리할 필요가 있을때는 편리하지만 1차열과 2차열의 위치를 모른다 