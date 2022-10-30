## 7장) 여러 데이터를 하나에 넣을 수는 없을까요?

#### 1.하나에 많은 것을 담을 수 있는 배열이라는게 있다는데
 ```
 int num[] = new int[3]; 
 num[0] = 1;
 num[1] = 2;
 num[2] = 3;
```
 - [] 안에는 아무것도 써주면 안됨.
 - 배열을 선언했으면, 초기화를 진행 해야한다.
 - 위에 선언된 num은 , 3개의 공간을 갖고 , 0~2까지의 index를 가지게 됨.
<table>
    <thead>
        <th>0번방</th>
        <th>1번방</th>
        <th>2번방</th>
    </thead>
    <tbody>
        <tr>
            <td>1</td>
            <td>2</td>
            <td>3</td>
        </tr>
    </tbody>
</table>

#### 2. 배열을 그냥 출력해보면 어떻게 나올까?

![img.png](../../../../../../JavaStudy/document/testImg/img.png)

** 위의 결과 같이,
 값을 지정해주지 않고 출력 할 시,
  `타입@주소값` 으로 출력이 됨.

#### 3. 배열을 선언하는 또 다른방법

```
int num[] = {1,2,3}
```
 - 선언과 동시에 값을 할당 해줄 수 있음.

```
int num[];
num = {1,2,3} 
```
 - 오류 발생 함. (선언과 동시에 값을 할당 해주지 않았기에)

#### 4. 알고는 있어야 하는 2차원 배열

```
int [][]num ;
num = new int[2][2];
```
 - 위와 같이 선언시 ,
   > num[0][0] , num[0][1] , num[1][0] , num[1][1] <br>
   > 4개의 저장공간이 생김. <br>
 - 선언시 참고
```
// 정상 작동
num = new int[2][];
// 오작동
num = new int[][];
// 오작동
num = new int[][2];

* 1차원 배열자리는 꼭 할당 선언을 해줘야 함을 알 수 있음. 
```

#### 5. 배열 길이는 어떻게 알 수 있을까요?
```
int[] num = new int[4];
System.out.println(num.length);        // 4 출력
```

#### 6. 배열을 위한 for문
```
for(타입이름 임시변수명 : 반복대상 객체) {
    로직실행!!
}
```

 - 사용 예시
```
int[] num1 = {1,2,3};
 for(int test : num1) {
 System.out.println("배열 for문  : " + test);
}
```

![img_1.png](../../../../../../JavaStudy/document/testImg/img_1.png)
