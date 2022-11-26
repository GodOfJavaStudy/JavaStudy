##6장
* if(boolean 값) 처리문장;
* if 다음에는 소괄호를 열고 닫아야 하며, 소괄호 안에는 boolean 형태의 결과가 있어야 한다.
  * 정확히는 소괄호 안의 결과가 true일 때 처리하는 '처리문장'과 세미콜론이 온다

```java
 public class ControlOfFlow{
    public static void main(String[] args) {
        ControlOfFlow control = new ControlOfFlow();
    }
    
    public void ifStatment(){
        if(true);
        if(true)
            System.out.println("It's true");
        
        if(true)
            System.out.println("it's also ture");
        
        if(false)
            System.out.println("it's false");
        
    }
}
```
* if문의 소괄호 뒤에는 기본적으로 어떤문장이 있든 간에 세미콜론이 하나만 있으면 된다
* 위를 실행 했을 떄 2개만 출력이 된다.
   * 위에는 true경우에만 if문을 처리하게 했고 마지막 false일 경우에만 출력을 하는데 false결과물이 없어서 출력이 안된다

> if(boolean) 처리문장1  
> else 처리문장2
* else는 (이미 언급 된 것에 덧붙여)또다른 , 다른 이라는 뜻이므로 if문장의 결과가 false일 때 처리하는 용도로 사용된다
  * if 조건이 true일 때 처리문장1을 실행하고 false일때는 처리문장2를 실행한다

```java
    public void ifStatment2(){
        int intValue = 10;
        if(intValue > 5)
            System.out.println("it's bigger than 5");
         else 
            System.out.println("it' smaller or equal than 5");
        

        if(intValue <= 5)
            System.out.println("it' smaller or equal than 5");
        else 
            System.out.println("it's bigger than 5");
        
    }
```

> it's bigger than 5  
> it's bigger than 5
* intValue가 5보다 크기 때문에 위의 결과로 출력이 된다
* intValue를 5로 할당하고 컴파일을 하면 it' smaller or equal than 5 의 결과 가 나온다

### if문을 다양하게 
* 위의 방식은 if 처리를 해야하는 문장이 하나일 경우에만 하고 대부분은 아래처럼 이용한다
> if (boolean값) {  
> 처리문장 1  
> 처리문장 2   
> }

* 위와 같이 if문의 조건이 있는 소괄호 뒤에 중괄호를 열고 닫으면 된다 
   * 조건이 ture일 경우에만 중괄호 안의 내용이 실행된다 else도 마찬가지로 똑같이 사용할 수 있다

> if (boolean값) {  
> 처리문장1  
> 처리문장2  
> } else {  
> 처리문장3  
> 처리문장4  
> }
 * 중괄호를 사용하는 것이 코드 가독성에도 좋다

```java
public class ControlOfFlow{
    public void ifStatement3(){
        int age = 25;
        boolean isMarride = true;
        
        if(age > 25 && isMarride) {
            System.out.println("age is over 24 && marride");
        }
    }
}
```
* &&는 두개의 조건이 true일 때 경우에만 true의 결과를 내준다 || 는 둘 중 하나라도 true만 있으면 된다 
* 위를 컴파일 할 경우 한개만 true이기 때문에 출력되는 것이 없다

```java
public class ControlOfFlow{
    public void ifStatement3(){
        int age = 25;
        boolean isMarride = true;
        
        if(age > 25 && isMarride) {
            System.out.println("age is over 25 or marride");
        }

        if(age > 25 || isMarride) {
            System.out.println("age is over 25 or marride");
        }
    }
}
```
* 위를 컴파일 할 경우 age is over 24 && marride 가 출력이 된다 
* || 조건은 두개의 boolean 값 중 하나만 true만 있으면 true가 되기 대문이다 
  * 자바에서는 &&의 경우에는 앞에 있는 조건이 false이면 그 겨로가도 false이기 때문에 두번째 조건은 묻지도 않는다 
  * ||에서는 앞에 조건이 true이면 뒤에 조건을 따지지 않고 결과가 true가 된다

```java
public class ControlOfFlow{
    public void ifStatement3(){
        int age = 25;
        boolean isMarride = true;
        
        if(age > 25 && isMarride) {
            System.out.println("age is over 25 or marride");
        }

        if(age > 25 || isMarride) {
            System.out.println("age is over 25 or marride");
        }
        
        double height = 180;
        if(age > 25 || isMarride && height >= 180) {
            System.out.println("age is over 25 or marride ane height is over 180");
        }

        if((age > 25 || isMarrid) && height >= 180) {
            System.out.println("age is over 25 or marride ane height is over 180");
        }
    }
}
```
* 위처럼 조건을 여러개 줄 때 어떤것이 먼저인지 헷갈리기 때문에 ()를 써서 묶어주는 것이 좋다
   * 괄호를 묶어주나 묶어주지 않으나 결과는 같다

```java
public class ControlOfFlow{
    public void ifStatement4(int point){
        if(point > 90){ // 90점 이상일 경우
            System.out.println("A");
        } else if(point > 80) { // 90이상은 아니지만 80점 이상일 경우 
            System.out.println("B");
        } else if (point > 70) { // 80이상은 아니지만 70점 이상일 경우 
            System.out.println("C");
        } else if (point > 60) { // 70이상은 아니지만 60점 이상일 경우 
            System.out.println("D");
        } else { // 60점 이상이 아닐 때 
            System.out.println("F");
        }
    }
}
```
 * else if 구문을 쓰면 지금까지의 조건이 맞지 않는 다른 조건을 찾는데 유용하다
```java
public void ifStatement4(int point){
        if(point > 90){ // 90점 이상일 경우
        System.out.println("A");
        } else if(point > 80) { // 90이상은 아니지만 80점 이상일 경우 
        System.out.println("B");
        } else if (point > 70) { // 80이상은 아니지만 70점 이상일 경우 
        System.out.println("C");
        } else if (point > 60) { // 70이상은 아니지만 60점 이상일 경우 
        System.out.println("D");
        } else { // 60점 이상이 아닐 때 
        System.out.println("F");
        }
        
        // if else if를 쓰지 않았을 경우
        if(point > 90){
        System.out.println("A"); 
        } else {
            if(point > 80){
             System.out.println("B");   
            } else {
                if(point > 70){
                System.out.println("C");  
                } else {
                    if(point > 60){
                    System.out.println("D");
                    } else {
                    System.out.println("F");
                    }
                  }
                }   
             }

        if(point >= 90){ // 90점 이상일 경우
        System.out.println("A");
        } 
        if(point < 90 && point >= 80) { // 90이상은 아니지만 80점 이상일 경우 
        System.out.println("B");
        } 
        if (point < 80 && point >= 70){ // 80이상은 아니지만 70점 이상일 경우 
        System.out.println("C");
        }
        if (point < 70 && point >= 60) { // 70이상은 아니지만 60점 이상일 경우 
        System.out.println("D");
        } 
        if (point > 60) { // 60점 이상이 아닐 때 
        System.out.println("F");
        }
        
         }
```

### switch문
```java
switch(비교대상변수){
    case 점검값 :
        처리문자 ;
        break;
    case 점검값2 :
        처리문자2 ;
        break;
    default:
        기본처리문장;
        ....
        break;
        }
```
* 가장 첫 줄에는 switch(비교대상변수)라고 명시한 후 중괄호를 시작한다. 
   * 여기서 괄호 안의 비교대상변수는 long을 제외한 정수형과 몇몇 특별한 타입만이 들어갈 수 있다
   * 여기서 중괄호는 if문장 처럼 생략하면 안된다
* 중괄호 안에는 case :  점검값 이 오거나 default가 나와야만 한다
   * 만약 case문장이 없으면 switch문을 쓸 필요가 없기 때문에 반드시 있어야 된다 
   * case문을 마무리 하고 싶다면 break를 추가해주면 된다
* 모든 조건이 끝나면 중괄호를 닫아준다

```java
public class ControloFlos{
    public void switchStatemnt(int num){
        switch (num)
        case 1:
        System.out.println("it is one foot bicycle");
        break;
        case 2:
        System.out.println("it is a motor cycle or bicycle");
        break;
        case 3:
        System.out.println("it is s three wheel car");
        break;
        case 4:
        System.out.println("it is a car);
        break;
        default:
        System.out.println("it is expensive car);
        break;
    }
}
```
* 메소드를 호출 할 때 1을 넣고 넘겨주면 it is one foot bicycle 가 출력된다
* case에 해당하는 값에 걸리면 case의 골론 뒤에 있는 문장이 실행되고 break라고 되어있기 때문에 switch문을 빠져나간다
* default는 앞에 있는 조건이 맞지 않는 경우에 수행된다 즉 모든 case의 조건이 맞지 않는 경우에만 실행된다
```java
public class ControloFlos{
    public void switchStatemnt(int num){
        switch (num)
        case 1:
        System.out.println("it is one foot bicycle");
       // break;
        case 2:
        System.out.println("it is a motor cycle or bicycle");
      //  break;
        case 3:
        System.out.println("it is s three wheel car");
        break;
        case 4:
        System.out.println("it is a car);
        break;
        default:
        System.out.println("it is expensive car);
        break;
    }
}
```
> it is one foot bicycle  
> it is a motor cycle or bicycle
> it is s three wheel car
* switch에서는 한번 조건을 반드시 시켜줬다면 다음에는 break가 나올 때 까지 실행된다 
* default는 마지막에 쓰는 것이 좋다

### 반복문
* 자바에는 for루프와 while문 두개의 반복문이 있다
>while(boolean 조건) {  
> 처리문장;  
> }
* while 후에 오는 소괄호 안에는 boolean조건이 있어야 된다
* boolean의 값이 true일 경우에만중괄호 안에 있는 내용들이 수행된다
  * 조건 결과 값이 false일 경우에는 아예 while문장이 수행되지 않는다
* while과 같은 반복문은 중괄호가 끝난 이후에 다시 boolean조건을 확인해 보고 이 값이 true이면 중괄호 안의 내용이 실행된다

```java
public class Control{
    public void whileLoop(){
        int loop = 0;
        while(loop < 12){
            loop++;
            switchStatment(loop);
        }
    }
}
```
* while문의 조건문 안에는 loop가 12보다 작으면 true가 되도록 지정을 해놓았다 loop값이 12를 넘으면 수행되지 않는다
* while문에서 break도 쓸 수 있고 메소드에서 빠져나갈 수 있다


```java
public class Control{
    public void whileLoop(){
        int loop = 0;
        while(loop < 12){
            loop++;
            if(loop == 6){
                continue;
            }
            switchStatment(loop);
        }
    }
}
```
* 반복문에서 countinue를 마난게 되면 그 이후에 있는 문장들이 수행이 안되고 바로 반복문의 boolean의 조건을 점검하는 곳으로 간다
* break문은 반복문을 빠져나가지만 countinue를 만나면 boolean 조건으로 가게 된다

#### for문
>for(1초기화 ; 258종료조건; 47조건값 증가){  
>  36반복문장   
> }
1. 초기화라고 되어 있는 부분에서는 변수를 초기화 한다
2. 종료조건 구문이 수행된다 이 종료 조건 내의 결과는 if문과 동일하게 boolean타입만 위치할 수 있다 이 boolean값이 true이면 for루프 내의 반복문장이 수행되고 그렇지 않으면 for는 종료된다
3. 종료조건 결과가 true이면 반복문이 수행된다
4. 중괄호 내의 작업이 종료되면 반복문장이 수행된다 보통은 초기화에서 선언한 변수를 여기서 증가시킨다
5. 반복문장을 수행하기 전에 다시 종료조건에 맞는지 확인한다
6. 앞선 조건 결과가 true일 경우에는 바나복문장을 다시 수행한다
7. 조건값 증가가 다시 수행된다
8. 종료조건을 만족하는지 확인한다
9. 조건 결과가 false일 경우에는 for 루프는 끝나고 다음 문장이 수행된다