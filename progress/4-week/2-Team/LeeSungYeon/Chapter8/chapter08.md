## 8장) 참조 자료형에 대해서 더 자세히 알아봅시다

#### 1. 기본 생성자
 - 클래스의 객체를 생성하기 위해 존재 해야함.
 - 생성자는 리턴타입x -> 리턴타입은 클래스의 객체 이기 때문.
 - 생성자는 클래스내의 메소드 중 최상단에 구현하는것이 적합.

#### 2. 생성자는 몇 개까지 만들 수 있을까?
- DTO vs VO 
  * DTO : 데이터를 다른 서버로 전달하기 위한 것이 주 목적 
  * VO : 데이터를 담아 두기 위한 목적

<span> 예시) 생성자 생성</span>
<br/>
<span> ** class명 생략 ** </span>

```
public String name;
public String phone;
public String email;
    // 아무정보도 없는 경우
    public MemberDTO() {}
    public MemberDTO(String name) {
        // 이름만 아는 경우
        this.name = name;
    }

    public MemberDTO(String name,String phone) {
        // 이름 , 번호만 알고 있을 때
        this.name = name;
        this.phone = phone;
    }

    public MemberDTO(String name,String phone,String email) {
        // 세가지 정보를 알고 있을 때
        this.name = name;
        this.phone = phone;
        this.email = email;
    }
```
  * 위에 예시에서 보듯이 생성자의 개수는 제한이 없다.
  * 필요에 따라 맞는 생성자를 생성하여 사용 할 수 있다.
  * <span style='color:orange'>참고) </span>생성시 생성자들이 필요한지 생각 해야함.
  * <span style='color:orange'>참고) </span>해당 클래스에 적합한 생성자 인지도 생각 해야함.

#### 3. 객체의 변수와 매개 변수를 구분하기 위한 <span style='color:orange'> this !! </span>
 - this 예약어는 생성자와 메소드 안에서 사용 가능
 ```
 public String name;
 public MemberDTO(String name) {
    // 이름만 아는 경우
   name = name;
   }
```
 -> 위와 같이 사용 시, 자바 컴파일러는 인스턴스 변수 = 매개변수 (name) 으로 생각하여 사용 불가능.

 -> 매개변수명을 바꿔 사용하면 정상 작동하지만, 것보단 this 예약어를 사용함.

 -> name = name이 아닌 , this.name = name 으로 선언 시 
    현재 객체의 name이라고 명시 해주는 것 

#### 4. 메소드 overloading

<span>예시) overloading</span>
```
public void print(int data) {}
public void print(String data) {}
public void print(int intData,String stringData) {}
public void print(String stringData,int intData) {}
```
-> 위의 예시와 같이, 메소드명은 같으나 매개변수를 다르게 구현하는것을 오버로딩 이라 함.

#### 5. 메소드에서 값 넘겨주기
 - 메소드의 수행과 종료<br>
   1.메소드의 모든 문장이 실행 되었을 경우 <br>
   2.return 문장에 도달했을 경우 <br>
   3.예외 발생한 경우 <br>

#### 6. static 메소드
 - static 메소드
   - 객체를 생성하지 않고 호출 가능.
   - 클래스 변수만 사용가능.
#### 7. static 블록
```
static {
    // 한번만 수행되는 로직
}
```
 - static 블록
   - 한 번만 호출 되어야 하는 코드라면 static 블록 사용
   - 객체가 생성되기 전에 한 번만 호출 됨
   - 클래스 내에 선언되어 있어야 함
   - 메소드 내에 선언 불가
   
### 8.pass by value
 - 값을 전달하는 작업
 - 호출 전,후 데이터가 변경 되지 않음. 즉, 기존값이 바뀌지 않음

```
public void callPassValue() {
        int a = 10;
        String b = "b";

        System.out.println("before");
        System.out.println("a : " + a); // 10 출력
        System.out.println("b : " + b); // b 출력

        passByValue(a,b);
        System.out.println("after");
        System.out.println("a : " + a); // 10 출력
        System.out.println("b : " + b); // b 출력
    }

    public void passByValue(int a, String b) {
        a = 20;
        b = "z";
        System.out.println("int passByValue");
        System.out.println("a : " + a); // 20 출력
        System.out.println("b : " + b); // z 출력
    }
```
#### 9. pass by Reference
 - 객체에 대한 참조가 넘어가는 것
```
public void callPassByRef() {
        MemberDTO member = new MemberDTO("성연1");
        System.out.println("before");
        System.out.println("name" + member.name); // 성연1 출력

        passByRef(member);
        System.out.println("after");
        System.out.println("name" + member.name); // 성연2 출력
    }

    public void passByRef(MemberDTO member) {
        member.name = "성연2";
        System.out.println("in passByRef");
        System.out.println("name : " + member.name); // 성연2 출력
    }
```
 ** 결론 
      - > value는 호출 전,후로도 값이 변경되지 않지만 reference는 값이 변경됨.
