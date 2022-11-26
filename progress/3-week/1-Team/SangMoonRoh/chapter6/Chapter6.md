# 제가 조건을 좀 따져요

- if문의 경우 영문법상 if + S + V , S + V로 작성한다.

#### if문 표기법 케이스

```java
public class IfMethod {

    public static void main(String[] args) {
        if (true) ;
        if (true) System.out.println("It's true");
        if (true)
            System.out.println("It's also true");
        if (false) System.out.println("It's false"); // 출력 되지 않음.
        // if 다음에 오는 소괄호 안에 값이 ture일 경우에만 처리된다. 
    }
}
```

### if 문에 여러 조건

- if문의 조건문 소괄호 안에 && 와 ||를 활용하면 여러 가지 조건을 한 번에 따질 수 있다.

```java
public class ControlIfAndOr {
    public static void main(String[] args) {
        ControlIFAndOr control = new ControlIfAndOr();
        control.ifAndOr();
    }

    public void ifAndOr() {
        int age = 25;
        boolean isMarried = true;

        if (age > 25 && isMarried) {
            System.out.println("Age is over 25 and Married");
        }
        if (age > 25 || isMarried) {
            System.out.println("Age is over 25 or Married");
        }
    }

}
```

- && 의 경우 앞에 있는 조건이 false이면 그 결과도 false이기 때문에 두번째 조건은 따지지 않는다.
- ||의 경우에는 첫번째 조건이 true이면 두 번째 조건은 신경 쓰지 않고 넘어간다.
- && || 혼용 해서 사용 가능하지만, 순서는 괄호를 사용해서 명확히 해야한다.  
  `if((age > 25 || isMarrid) && height >= 180)`<br><br>
  `System.out.println( point > 80 ? "Good" : "Bad");`

```java
public class WhatISIF {
    public void elseIf2(int point) {
        String result = point > 90 ? "A" : point > 80 ? "B" : point > 70 ? "C" : point > 60 ? "D" : "F";
        System.out.println(result);
    }
}
```

- 이를 한 줄로 처리하면

```java
System.out.println(point>90?"A":point>80?"B":point>70?"C":point>60?"D":"F");
```

## Switch 문

```java
public class HowToUseSwitch {
    public static void main(String[] args) {
        switch ("비교대상변수") {
            case "점검값1":
                "처리문장1";
                //...
                break;
            case "점검값2" :
                "처리문장2";
                //...
                break;
                //...
            default:
                "기본처리문장";
                //...
                break;
        }
    }
}
```
- switch 문장 작성 순서
  - 가장 첫 줄 `switch`(비교대상 변수)라고 명시한 후 중괄호를 시작.
  - 괄호 안의 비교대상 변수는 `long`타입을 제외한 정수형과 몇몇 특별한 타입만이 들어갈 수 있다.
  - 중괄호 안에는 "`case 점검값:`"이 오거나, `default:`가 나와야만 한다.
  - `case`문장이 없으면 `switch`문을 쓸 필요가 없어서 반드시 있어야 한다.
  - `case`를 마무리 하고 싶다면 `break`는 필수이다.
  - 조건을 만족 시켰다면 그 다음 break가 올 때까지 어떤 case가 오든지 상관 하지 않고 계속 무사 통과하면서 실행함.

  - break를 사용하는 이유
```java
public class ControlOfFlow{
    public static void main(String[] args) {
        ControlOfFlow controlOfFlow = new ControlOfFlow();
        int month = 1;
        controlOfFlow.switchCalendar(month);
    }
    
    public void SwitchCalendar(int month){
        switch (month){
            case 1:
            case 3:
            case 5:
            case 7:
            case 8:
            case 10:
            case 12:
                System.out.println(month + " has 31 days. ");
                break;
            case 4:
            case 6:
            case 9:
            case 11:
                System.out.println(month + " has 30 days. ");
                break;
            case 2:
                System.out.println(month + " has 38 or 29 days. ");
                break;
            default:
                System.out.println(month + " is not a month. ");
                break;
        }
    }
}
```
- 위 예시처럼 특정 조건에 따른 처리를 해야할 경우 switch를 사용하면 좋다.
- Java 6 까지는 switch 문에서는 long 을 제외한 정수와 Enum과 몇몇 몇몇 참조 자료형에서만 Switch 사용 가능.
- Java 7 부터는 String 도 Switch 사용 가능.
> * 참조 자료형 : Character, Byte, Short, Integer


## 반복문
 ### while 문
- boolean 조건이 소괄호에 있어야 한다.
- boolean 조건 값이 true 일때만 내용들이 수행된다.
- 조건 결과 값이 false 인 경우 아예 while 문장이 수행되지 않는다.
- if문과 다른점은 중괄호 안의 내용이 끝나면 그 다음 아래줄로 넘어가지만,  
while과 같은 반목문은 중괄호가 끝난 이후 다시 위로 올라가서 boolean  조건을 확인하고 이값이 true면 중괄호 안의 내용이 계속 실행된다.

```java
public class ControlWhile {
    public static void main(String[] args) {
        ControlWhile controlWhile = new ControlWhile();
        controlWhile.whileLoop1();
    }
    
    public void whileLoop1() {
        ControlSwitch controlSwitch = new ControlSwitch();
        int loop = 0;
        while (loop < 12 ){
            loop++;
            controlSwitch.SwithchCalender(loop);
        }
    }
}
```
- break : while 문 내에서도 break 사용해서 반복문을 빠져나올 수 있다. ( 조건문과 함께 사용)
- continue :  문장을 건너 뛸수 있는 예약어, continue 는 단순히 계속 진행 하라 X,   
boolean 조건 점검 부분으로 다시 가라는 의미
    - 매우 조심스럽게 사용 해야한다. 시점에 따라 실행결과가 달라질 수 있다.
    - 무한 루프에 빠질 수 있게 될 수 있다.
### do - while 문
```java
do {
    처리문장 ;
        .....
        } while (boolean조건);
```
- do- while 문은 적어도 반복 문장이 실행된다.  
while 문은 조건ㅇ ㅔ한번도 맞지 않으면 한번도 실행되지 않지만, do-while문은 "한 번은 꼭 실행시키고 싶을 때 사용".

### 가장 확실한 for 루프
- for 기본문
```java
 for (1.초기화; 2,5,8 종료조건; 4,7 조건 값 증가){
    3,6 반복문장
        }
        9
```
1. 변수를 초기화 한다.
2. 종료조건 구문 수행, 이 종료 조건 내의 결과는 if문과 동일하게 boolean 타입만 위치 가능  
boolean 값이 true이면 for 루프 내의 반복문장이 수행되고, 그렇지 않으면 for루프 종료.
3. 종료조건 결과가 true이면 "반복문장"이 수행된다.
4. 중괄호 내의 작업이 종료되면 "조건 값 증가" 가 수행된다.  
보통은 초기화 에서 선언한 변수를 여기서 증가.
5. 반복문장을 수행하기 전에 다시 " 종료조건"을 다시 수행한다.
6. 앞선 조건 결과가 true일 경우에는 반복문장을 다시 수행한다.
7. 조건값 증가가 다시 수행
8. 종료 조건을 만족하는지 확인한다.
9. 조건 결과가 false 일 경우에는 for 루프는 끝나고 다음 문장이 수행된다.

```java
public class ControlFor{
    public static void main(String[] args) {
        ControlFor controlFor = new ControlFor();
        controlFor.forLoop(10);
    }
    public void forLoop(int until){
        int sum = 0 ;
        for (int loop = 1; loop <=until; loop++) {
               sum+=loop;
        }
        System.out.println("1 to " + until + " = " + sum);
    }
}
```
- for 루프도 while문처럼 break, continue를 사용할 수 있다.

### label
- 두개 이상의 for 나 while 루프가 있을 때 사용된다.
```java
public class TimesTable{
    public void printTimesTableSkip4Case1(){
        for (int level = 2; level < 10; level++) {
            if (level==4) continue;;
            for (int unit = 0; unit < 10; unit++) {
                if(unit ==4 ) continue;
                System.out.println(level+ "*" + unit + "=" +level+unit+ " " );
            }
            System.out.println();
        }
    }
}
```
- System.out.println(); 문장을 거치지 않고 level을 사용하는 for루프로 바로 가려고하면  
label을 사용하면 된다.
- 다음과 같이 반복문 바로 앞에 원하는 이름(여기서는 startLabel)을 입력하고 콜론을 써주면 된다.
```java
public class PrintTime {
    public static void main(String[] args) {
    startLabel;
        for (int level = 2; level < 10 ; level++) {
            for (int unit = 1; unit < 10 ; unit++) {
                if (unit==4) continue startLabel;
                System.out.print (level + "*"+unit+"="+level*unit+" ");
            }
            System.out.println();
        }
    }    
} 
```