# 계산을 하고 싶어요 
- 연산자를 영어로 Operator  
대부분 연산자는 기본 자료형을 더하거나 빼는 등의 계산을 하기 위해서 사용한다.
- 기본 자료형을 제외한 참조 자료형은 연산자를 사용할 수 없지만 String 만 + 연산자 사용이 가능하다.
- 산술 연산자는 기본 자료형 중에서 boolean을 제외하 나머지 타입에서 사용할 수 있다.
<br><br>

### 등호 ( " = ")
 - 대입연산자 (assignment operator) : a=3와 같이 왼쪽에 변수에 오른쪽에 있는 값을 대입할 때 사용한다.

## 산술연산자
 - 더하기 연산자 (+) : additive operator)
 - 빼기 연산자 (-) : subtraction operator
 - 곱하기 연산자 (*) : multiplication operator
 - 나누기 연산자 (/) : division operator
 - 나머지 연산자 (%) : remainder operato


### ( +) 와 ( -)
```java
public class OperatorPlusMinus {
    public static public static void main(String[] args) {
        OperatorPlusMinus sample = new OperatorPlusMinus();
        sample.additive();
    }
    
    public void additive(){
        int intValue1 = 5;
        int intValue2 = 10;
        
        int result = intValue1 + intValue2;
        System.out.println(result);
        result = intValue2 - intValue1;
        System.out.println(result);
    }
    
}
```

### ( *)와 ( /)
- 여기에 곱하기 ( *) 와 나누기 ( /) 계산을 하는 multiplicative() 라는 메서드를 추가해보자.
```java
public class OperatorPlusMinus {
    public static public static void main(String[] args) {
        OperatorPlusMinus sample = new OperatorPlusMinus();
        sample.multipleDivision();
    }
    
    public void multipleDivision(){
        int intValue1 = 5;
        int intValue2 = 10;
        
        int result = intValue1 * intValue2;
        System.out.println(result);
        result = intValue2 / intValue1;
        System.out.println(result);
    }
    
}
```
- 위의 코드 결과는 각각 50 2 가 된다.

#### 왜 0 intValue2 / intValue1로 썼을까?
- 만약 반대로 intValue1/intValue2  5/10 이라면 0.5가 아닌 0 이 나온다.
- 이런 경우 계산하려면 double이나 float형으로 계산하면 된다. 
```java
public class OperatorPlusMinus {
    public static public static void main(String[] args) {
        OperatorPlusMinus sample = new OperatorPlusMinus();
        sample.multipleDivision();
    }
    
    public void multipleDivision(){
        double intValue1 = 5;
        double intValue2 = 10;
        
        double result = intValue1 * intValue2;
        System.out.println(result);
        result = intValue2 / intValue1;
        System.out.println(result);
    }
    
}
```

### ( %) 
- remainder operator
- %는 백분율을 나타내는 퍼센트 기호 X
- 나머지를 뜻하는 기호
```java
public class OperatorRemainder {
    public static void main(String[] args) {
        OperatorRemainder sample = new OperatorRemainder();
        sample.remainder();
    }
    
    public void remainder() {
        int intValue1 = 53;
        int intValue2 = 10;
        int result = intValue1 % intValue2;
        System.out.println(result); // 3
    }
}
```
- 이 remainder() 메소드만 main() 메서드에서 호출하도록 하고, 앞에서 사용한 메서드 호출 부분은 주석 처리한 후 결과를 확인해보자.
 100이 18의 배수인지 확인 할수 있는 방법을 생각해면 % 연산자가 없다면 그 결과를 쉽게 생각하기 어려울 것.  
100 % 18의 결과가 0인지 아닌지만 확인하면, 18의 배수인지 쉽게 알 수 있다.

### 간단하게 계산하는 복합 대입 연산자들 
- 복합 대입 연산자 (Compound Assignment Operator)
```java
int intValue = 10;
intValue = intValue + 5;
```
이렇게 계산하면, intValue의 원래 값은 10이지만, 5를 더해서 15가 된다.  
이처럼 자신의 값에 특정 값을 더할 필요가 있는 경우에는 다음과 같이 간단하게 처리할 수 있게 된다.
```java
int intValue = 10;
intValue += 5;
```  
- +와 = 사이에 공백이 있어서는 안됨. 두기호를 붙여 써야한다.
"intValue"에 5를 더한 것을 intValue에 할당해라." 라는 의미다. 이러헤 사용할 수 있는 연산자 앞절에서 배운 5가지 이다.
  - += : 기존 값에 우측 항의 값을 더함.
  - -= : 기존 값에 우측 항의 값을 뺌.
  - *= : 기존 값에 우측 항의 값을 곱함.
  - /= : 기존 값을 우측 항의 값으로 나눔.
  - %= : 기존 값을 우측 항의 값으로 나눈 나머지.
```java
 public class OperatorCompound(){
    public static void main(String[] args) {
        int intValue = 10; // 1. 정수형인 intVlaue를 선언하여 10을 할당하자.
         intValue += 5;
         System.out.println(intValue); //2.5를 더하고 결과를 출력
         intValue -= 5;
         System.out.println(intValue); //3. 2의 결과에서 5를 빼고 결과를 출력
         intValue *= 5;
         System.out.println(intValue); //3. 2의 결과에서 5를 곱하고 결과를 출력
         intValue /= 5;
         System.out.println(intValue); //3. 2의 결과에서 5를 나누고 결과를 출력
         intValue %= 5;
         System.out.println(intValue); //3. 2의 결과에서 5로 나눈 나머지 값의 결과를 출력
    }
}
```


## 피연산자가 하나인 단항 연산자
- (+ ) : 단항 플러스 연산자. Unary plus opeartor 
- (- ) : 단항 마이너스 연산자. Unary minus operator
- (++ ) : 증가 연산자. Increment operator
- (-- ) : 감소 연산자. Decrement operator
- (! ) : 논리 부정 연산자. Logical complement operator

### + 와 -
```java
public class OperatorUnary {
  public static void main(String[] args) {
    OperatorUnary operatorUnary = new OperatorUnary();
    operatorUnary.unary();
  }
  
  public void unary() {
      int intValue =-10;
      int result = +intValue;
      System.out.println(result);
      result = - intValue;
      System.out.println(result); 
  }
}
```
- 이렇게 두 개의 숫자나 변수를 비교하는 것이 아니라, 단 하나의 숫자나 변수 앞에 +나 -를 붙이면 단항 연산자로 처리되는 것이다.
  - (+ ) 는 변수x(1)를 의미.
  - (- ) 는 변수x(-1)를 의미.
```java
int intValue=+3; // 양수 3
```
### ++와 --
- `Unary` 메서드에 `intValue`의 1만큼 증가시키고, 1만큼 감소시키려면 다음과 같다.
```java
intValue = intValue+1;
intValue = intValuye-1;

intValue++; // 단 숫자가 아닌 변수에만 사용가능
intValuye--; // 단 숫자가 아닌  변수에만 사용가능
```

#### ++ -- 를 앞에 붙이는 것과 뒤에 붙일 때 어떤 차이가 있을까?
- 앞에 붙이면 그 변수를 참조하기 전에 1을 더한다.
- 뒤에 붙이면 변수를 참조한 후에 1을 더한다.
- increment() 메서드를 만들고, main() 메서드에 이 메서드만을 호출하도록 변경한 후 실행해보자.
```java
public class OperatorIncrement {
    public static void main(String arg[]){
            OperatorIncrement operator = new OperatorIncrement();
            operator.increment();
    }
    public void increment(){
        int intValue = 1;
      System.out.println(intValue++);
      System.out.println(intValue);
      System.out.println(++intValue);
    }
}
```
- 이렇게 하면
  - 첫 번째 System.out.println()을 수행하여 결과를 출력한 후에 1을 더하고,
  - 두 번째 출력에서는 그냥 값만 출력.
  - 세 번째 출력문을 수행하기 전에 1을 더하고 결과를 출력한다.

### ! 
 - boolean 앞에 붙여주면 결과가 반대가 된다.
```java
public class OperatorComplement {
  public static void main(String[] args) {
    OperatorComplement operator = new OperatorComplement();
    operator.complement();
  }
  public void complement() {
      boolean flag = true;
      System.out.println(flag);
      System.out.println(!flag);
  }
}
```


### 자바에서 계산 하는 순서 
```java
1 + 2 * 3 
```

```java
( 1+2 )* 3
```
수학 공식에서의 계산과 동일 * / 먼저 계산하거나 괄호가 있을 경우 괄호 안을 먼저 계산

### 자바에서의 연산자의 우선순위
|구분|연산자|우선 순위|
|-----|-----|-----|
|단항 연산자| ++ == + - ! ~ |1|
|산술 연산자| * / % | 2|
|     "    |+ - | 3|


### ~ 도 연산자다 ( 틸드)
- 2 진수로 되어 있는 비트 값을 전부 거꾸로 바꾸는데 사용한다.
- ~ 는 비트 값의 0을 1로, 1을 0으로 바꾸는데 사용한다.
```java
public class OperatorTilde {
  public static void main(String[] args) {
    OperatorTilde operator = new OperatorTilde();
    byte b = 127;
    operator.printTildeResult(b);
    // Original value = 127
    //Tilde value = -128
    b = 1;
    operator.printTildeResult(b);
    // Original value = 1
    //Tilde value = -2
  }
  
  public void printTildeResult(byte b){
      System.out.println("Original value = "+b);
      System.out.println("Tilde value = "+~b);
  }
}
```

### 비교 연산자
 - (== ) : 같음 (equal to)
 - (!= ) : 같지 않음(not equal to)
 - (> ) : (왼쪽 값이) 큼 (greater than)
 - (>= ) : (왼쪽 값이) 작음(greater than or equal to)
 - (< ) : (왼쪽 값이) 작음 (less than)
 - (<= ) : (왼쪽 값이) 같거나 작음 (less than or equal to)
   - 위의 비교 연산자의 결과 값은 반드시 boolean이다.

### ==과 != ( Equality Operator)
 - == 와 != 는 "등가 비교 연산자"라고 한다.
 - 두 개의 값이 같은지, 다른지를 확인 할 때 사용된다.
```java
public class OperatorComparision {
  public static void main(String[] args) {
    OperatorComparision operator = new OperatorComparision();
    operator.comparision();
  }
  
  public void comparision(){
      int intValue1= 1;
      int intValue2= 2;
      int intValue3= 3;
      
      System.out.println(intValue1==intValue2); //false
      System.out.println(intValue1==intValue3); // true
   
      System.out.println(intValue1!=intValue2); // true
      System.out.println(intValue1!=intValue3); // false
  }
}
```

- 이 등가 비교 연산자는 모든 타입에서 사용 가능하다.
  - 모든 기본 자료형과 참조 자료형에서 사용 가능하다.
  - 기본 자료형은 같은 종류끼리 비교가 가능하다. 
    - char == int, double == int, boolean == boolean과 같이 비교할 수 있다.
    - boolean == int , boolean == char와 같이 사용 할 수 없다.
```java
public class OperatorComparison{
  public static void main(String[] args) {
    OperatorComparison operator = new OperatorComparison();
    //operator.comparison();
    operator.comparison2();
  }
  
  public void comparison2{
      //내용 사ㅐㅇ략
  }
  
  public void comparison2() {
      char charValue = 'a';
      System.out.println(97==charValue);
      int intValue = 1;
      double doubleValue = 1.0;
      System.out.println(intValue == doubleValue);
  }
}
```
- cahr 타입으로 'a'의 int  값은 97이다. 따라서 필자가 숫자끼리는 서로 비교할 수 있다는 말이 맞다면 이 결과가 true가 나와야 하며,  
double 도 1.0이기 때문에 int 1과 같다고 나와야하지만 정상이다.

### <,>, <=, >=
 - 이 네 개 연산자는 두 개의 값이 큰지 작은지를 비교하는 데 사용되며 "대소 비교 연산자"라고 부른다.
 - 영어로는 Relational Operator 라고 부른다. 두 개의 값이 서로 큰지 작은지를 비교하 하는 것이기 때문에 숫자에서만 사용 가능하다. 
 - 각 연산자의 true 조건을 정리해 보면 다음과 같다.
 - ( =<) 나 ( <=)의 경우 두 기호의 순서가 다르면 안된다.

|연산자|사용 가능한 타입|
|-----|---------------|
|==, !=|모든 기본 자료형과 참조 자료형 -> 즉 모든 타입|
| >,<,>=,<= | boolean을 제외한 기본 자료형|

### 논리 연산자 (Conditional Operator)
 - && : AND 결합. Conditional AND
 - || : OR 결합. Conditional OR

### 아주 특이한 ? : 삼항연산자  Conditional operator ?: 
```java
public class OperatorConditionalTriple {
    public boolean doBlindDate(int point){
        boolean doBlindDateFlag = false;
        doBlindDateFlag = (point +" : " + doBlindDateFlag);
        return doBlindDateFlag;
    }
    
}
```
`변수 = (boolean조건식) ? true 일때 값 : false 일때 값 ;`
- 삼항 연산자는 = 왼족에 있는 변수에 값을 할당할 때 사용.
- 변수 우측에는 할다응ㄹ 위한 = 를 사용해야 한다. =와 ? 사이에는 앞 절에서 배운 boolean 타입의 결과를 제공하는 조건식이 있어야 한다. 
- 괄호 안의 값은 반드시 boolean 타입 결과를 제공 
- 순서대로 ? 의 우측에는 true일 때 값.
- : 우측에는 false일 때의 값을 지정해 둔다.
- 할당되는 값은 = 왼쪽에 있는 것과 같은 타입이면 된다.

### instanceof 라는 연산자와 비트 연산을 하는 78개의 연산자.
- instanceof 가 기호로 안되어 있어 연산자로 인정할수 없다는 의견도 있을 수 있다.
- 유일하게 자바의 예약어로 되어 있는 연산자가 바로 instanceof.

### 형변환 (캐스팅;casting)
- 형 변환은 서로 다른 타입 사이에 변환하는 작업을 하는 것을 말한다. 
- 기본 자료형과 참조 자료형 모두 괄호로 묶어주면 된다.
- boolean은 형변환이 되지 않는다.
- 기본 자료형 -> 참조 자료형, 참조 자료형 -> 기본 자료형으로의 형변환은 절대 안 된다.
- 숫자 값을 참조형으로 바꾸는 방법이 아예없진 않다.
- 각 타입 별로 값을 지정할 수 있는 범위가 정해져 있다.
  - byte 타입으로 할당한 변수를 short 타입의 변수로 지정하고 싶을 때
  - short 타입으로 할당한 변수를 byte 타입의 변수로 지정하고 싶을 때
- byte에서 short로 변환되는 것과 같이 1바이트에서 2바이트 짜리 타입으로 바이트 크기가 커지는 캐스팅을 할 경우에는 별도로 해줄 것이 없다.
- 2바이트짜리인 short에서 1바이트인 byte로 형 변환을 한다고 생각해보자. 생각만 해도 약간 복잡해질 것 같다.
```java
public class OperatorCasting{
    
public static void main(String[]args){
        OperatorCasting operator = new OperatorCasting();
        operator.casting();
        }
        public void casting(){
    byte byteValue = 127; // byte최대값인 127할당
    short shortValue = byteValue; // byte 값을 shortValue 라는 변수에 할당.
          // 이와 같이 범위가 작은 타입에서 범위가 큰 타입으로 변활 할때에는 별도도로 명시 하지 않아도 형변ㅅ화가 이뤄진다.
          //bsilFD순서로 형변환을 할때는 아무런 문제가 없다. 
    
          
    shortValue++;// shortValue에 1을 더하ㅣ고 결과를 출력했다.
    System.out.println(shortValue);
    byteValue = (byte) shortValue; // byteValue 변수에 byte의 최대값 보다 1이 많은 shortValue를 할당했다.
    System.out.println(byteValue); // 값 -128 게다가 shortValue 앞에는 (byte) 라고 씌어 있다.
          // 이와 같이 범위가 큰 타입에서 범위가 작은 타입으로 변환할 때에는 소괄호 안에 범위가 작은 타입을 명시해주어야만 한다. 그렇지 않으면 컴파일 에러
        }
        }
```
- short에서 byte로 변환한다는 것은 short의 앞에 있는 1바이트 (8비트)를 그냥 버리기 때문에 byte로 형 변환한 결과는 다음과 같다.
- byte의 가장 첫 bit가 1이면 그 값은 -128이다. 그렇기 때문에 결과가 -128로 나온다.
- 2^8위치에 있는 값만 1인 short를 생각해보자, 1바이튼버린다고 했는데, 이 경우에는 1바이트를 버리면 나머지 자리에는 모두 0밖에 안남는다. 
```java
public class OpertatorCasting {
  public static void main(String[] args) {
    OpertatorCasting opertator = new OpertatorCasting();
    // operator.casting ();
    opertator.casting2();
  }
  
  public void casting2() {
      short shortValue = 256;
      byte byteValue = (byte) shortValue;
      System.out.println(byteValue);// 0
      shortValue = 255;
      byteValue = (byte) shortValue;
      System.out.println(byteValue); // -1
  }
}
```

### 타입 별 사용 가능한 연산자 알아보기
| 구분                | -- | 연산자                   |
|-------------------|----|-----------------------|
| 결과가 boolean인 경우   |숫자 비교 연산자| <,<=,>,>=             |
| "                 |숫자 동등 연산자| == , !=               |
| 결과가 int나 long인 경우 | 기본 사칙 연산자| +,-,*,/,%             |
| "                 |증감 연산자 | ++, --                |
 | "                 | 비트 연산자 | &,^,~,<<, >>, >>> ,\^ |
| 기타 연산자 | 삼항 연산자 | ?:                    |
|"|형 변환 연산자 | (타입)                  |
|"|문자열 더하기 | +                     |

### 소수점 타입 연산자 
| 구분                | -- | 연산자      |
|-------------------|----|----------|
| 결과가 boolean인 경우   |숫자 비교 연산자| <,<=,>,>= |
| "                 |숫자 동등 연산자| == , !=  |
| 결과가 int나 long인 경우 | 기본 사칙 연산자| +,-,*,/,% |
| "                 |증감 연산자 | ++, --   |
| 기타 연산자            | 삼항 연산자 | ?:       |
| "                 |형 변환 연산자 | (타입)     |
| "                 |문자열 더하기 | +        |
- 정수형 타입과 비교해보면, double 과 float은 소수형이기 때문에 비트 연산이 불가능하다.

### boolean 타입에 대한 연산자들을 살펴보자.
| 구분 | 연산자 | 
|------|-------|
|동등연산자| ==, !=|
|조건적 논리 연산자| &&, \\|
|논리 연산자| !, &, \, ^|
|삼항 연산자| ? : |
|문자열 더하기 연산자 | +|

- & , \, ^ 은 숫자에 사용하면 비트 연산, boolean 에 사용하면 논리 연산을, boolean 타입 사이에 사용하면 논리 연산을 수행한다.

|연산자| 내용                      |
|-----|-------------------------|
|& | 두 값이 모두 true일 경우에만 true |
|\^| 두 값이 모두 false일 경우에만 false|
|^ | 두 값이 서로 다를 경우에는 true, 모두 true이거나 false이면 false|

- && 와 &가, \^\^와 \^가 같아 보인다, 실제 연산하는 방식은 아주 큰 차이가 있다.
- &&의 경우 좌측에 있는 연산이 false이면 우측에 있는 연산을 수행하지 않는다.
- && 연산은 두개의 결과가 모두 true여야지만 결과가 true가 되므로 앞에 있는 결과가 false일 경우 뒤에 있는 연산을 수행할 필요가 없다.  
하지만 &의 경우에는 좌측 연산 결과와 우측 연산 결과를 비교해야만 하기 때문에 모든 연산을 수행한다. 
```java
System.out.println( (a==3) && (b==1))
```
이처럼 && 연산자를 사용하면 만약 a가 1이라서 false라면 우측에 있는 b==1 이라는 비교를 수행하지도 않는다.
```java
System.out.println( (a==3) & (b==1))
```
이 경우에는 좌우 둘다 연산한다.

