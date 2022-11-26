## 9장) 자바를 배우면 패키지와 접근 제어자는 꼭 알아야 해요

#### 1. 패키지는 폴더의 개념이 아니에요
 - 패키지 선언 시 제약사항
   - 소스의 가장 첫줄에 있어야 함.
   - 패키지 선언은 소스 하나에는 하나만 존재 해야 함.
   - 패키지 이름과 위치한 폴더 이름이 같아야 함.
   
#### 2. 패키지 이름은 이렇게 지어요.
<table>
    <thead>
        <th>패키지 시작 이름</th>
        <th>내용</th>
    </thead>
    <tbody>
        <tr>
            <td>java</td>
            <td>자바 <span style="color:orange;">기본</span> 패키지(java 벤더에서 개발)</td>
        </tr>
        <tr>
            <td>javax</td>
            <td>자바 <span style="color:orange;">확장</span> 패키지(java 벤더에서 개발)</td>
        </tr>
        <tr>
            <td>org</td>
            <td>일반적으로 비 영리단체(오픈소스)의 패키지</td>
        </tr>
        <tr>
            <td>com</td>
            <td>일반적으로 비 영리단체(회사)의 패키지</td>
        </tr>
    </tbody>
</table>

 - 패키지 이름 지정 시 유의사항 
   - 패키지 이름은 모두 소문자
   - 자바의 예약어 사용 불가능
 
#### 3. import를 이용하여 다른 패키지 접근하기
 - 단일 패키지 접근 : import "패키지이름.클래스이름"
 - 다중 패키지 접근 : import "패키지이름.*"
 - static 메소드,변수 접근 : import static "패키지이름.클래스이름"
 - 같은 패키지 내에서는 import 사용 하지 않음

#### 4. 자바 접근 제어자
 - public : 전체 접근 가능
 - protected : 같은 패키지 내 or 상속받은 경우 접근 가능
 - package-private : 같은 패키지 내 (접근 제어라는 적어 주지 않았을 경우) 접근 가능
 - private : 해당 클래스 내 접근 가능
 
<table>
    <thead>
        <th></th>
        <th>해당 클래스 내</th>
        <th>같은 패키지 내</th>
        <th>상속 클래스 내</th>
        <th>import한 클래스 내</th>
    </thead>
    <tbody>
        <tr style="text-align:center;">
            <td>public</td>
            <td>O</td>
            <td>O</td>
            <td>O</td>
            <td>O</td>
        </tr>
        <tr style="text-align:center;">
            <td>protected</td>
            <td>O</td>
            <td>O</td>
            <td>O</td>
            <td>X</td>
        </tr>
        <tr style="text-align:center;">
            <td>package private</td>
            <td>O</td>
            <td>O</td>
            <td>X</td>
            <td>X</td>
        </tr>
        <tr style="text-align:center;">
            <td>private</td>
            <td>O</td>
            <td>X</td>
            <td>X</td>
            <td>X</td>
        </tr>
    </tbody>
</table>
