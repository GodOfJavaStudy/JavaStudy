# 자바랭 다음으로 많이 쓰는 애들은 컬렉션 - Part2(Set 과 Queue)

## Set이 왜 필요하지?
- Collection을 확장한 배열과 비슷한 역할을 하는 3개의 인터페이스 List, Set, Queue
  - List는 순서가 중요한 데이터를 담을 때 사용
  - Set 은?
    - 순서에 상관없이 어떤 데이터가 존재하는지를 확인하기 위한 용도로 많이 사용된다.
    - 중복 방지/ 원하는 값 포함 여부 확인이 주용도.
      - ex ) 어떤 서버에 1분간 사용자가 요청한 로그가 있다.  
      이 서버에 붙어서 요청한 IP를 기준으로 사용자의 수가 얼마나 되는지 확인한다고 가정해보면,  
      1분간 동일한 서버에 요청하는 중복 사용자 수는 매우 많다. 이러한 경우에 만약 앞 장에서배운 배열로 확인하게 되면   
      indexOf()라는 메서드로 해당 객체가 존재하는지 확인 후 add() 메서드로 추가하는 작업을 반복해야만 한다.  
      하지만 Set 을 구현한 클래스를 사용하면 그냥 데이터를 추가만 해주면 중복되지 않고 저장된다.
      - HashSet의 예제
        - Set인터페이스를 구현한 주요 클래스는 HashSet, TreeSet, LinkedHashSet이 있다.
          - HashSet : 순서가 전혀 필요 없는 데이터를 해시 테이블 `hashTable`에 저장한다. Set중에 가장 성능이 좋다.
          - TreeSet : 저장된 데이터의 값에 따라서 정렬되는 셋이다. red-black 이라는 트리 타입으로 값이 저장된다. HashSet보다 약간 성능이 느리다.
          - LinkedHashSet : 연결된 목록 타입으로 구현된 해시 테이블에 데이터를 저장한다.
          - 저장된 수너에 따라 값이 정렬된다. 대신 성능이 가장 나쁨.
        - 성능 차이는 데이터 정렬 때문이다. HashSet은 별도의 정렬 작업이 없어 제일 빠르다.
        - red-black 트리는 가 노드의 색을 붉은 색 혹은 검은색으로 구분하여 데이터를 빠르고 쉽게 찾을수 있는 구조의 이진트리 ` 자가 균형 (높이 균형) 이진 탐색 트리`를 말한다.

### HashSet ? 
- HashSet 클래스의 상속 관계
```java
java.lang.Object
 - java.util.AbstractCollection<E>
    - java.util.AbstractSet<E>
        - java.util.HashSet<E>
```

- `AbstractCollection`을 확장한 것은 ArrayList와 동일하다.
- HashSet은 AbstractSet을 확장했다.
  - AbstractSet 클래스는 이름 그대로 abstract 클래스이다.
  - 구현되어 있는 메서드는 Object 클래스에 선언되어 있는 equals(), hashCode() 메서드와 이 클래스에서 추가한 removeAll()뿐이다.
  - Set은 무엇보다도 데이터가 중복되는 것을 허용하지 않는다. 데이터가 같은지를 확인하는 작업은 Set의 핵심.
    - equals()메서드와 hashCode() 메서드와 떨어질수 없는 불가분의 관계이다.
    - equals() 와 hashCode() 메서드를 구현하는 부분은 Set에서 매우 중요하다.
    - 추가로 removeAll() 메서드는 컬렉션을 매개 변수로 받아, 매개 변수 컬렉션에 포함된 모든 데이터를 지울 때 사용한다.
    - 상속 관계를 간단히 살펴보았으니, HashSet이 어떤 인터페이스를 구현했는가.
    - |인터페이스| 용도                                                         |
      |------------------------------------------------------------|---|
      |Serializable| 원격으로 객체를 전송하거나, 파일에 저장할 수 있음을 지정                           |
      |Clonable| Object 클래스의 Clone() 메서드가 제대로 수행될 수 있음을 지정 즉, 복제가 가능한 객체이다. |
      |Itrable<E>| 객체가 "foreach"문장을 사용할 수 있음을 지정.|
      |Collection<E>|여러 개의 객체를 하나의 객체에 담아 처리할 때의 메서드 지정|
      |Set<E>|셋 데이터를 처리하는 것과 관련된 메서드 지정|
  - Set은 순서가 없다. 순서가 매개 변수로 넘어가는 메서드나 수행 결과가 데이터의 위치와 관련된 메서드는 Set인터페이스에서는 필요가 없다.
  - get(int index), indexOf(Object o)와 같은 메서드들은 Set에 존재 하지 않는다.

### HashSet의 생성자들도 여러 종류가 있다.
- HashSet 클래스에는 다음과 같이 4개의 생성자가 존재한다.
  - |생성자|설명|
    |-----|----|
    |HashSet() |데이터를 저장할 수 있는 16개의 공간과 0.75의 로드 팩터(load factor)를 가즌 객체를 생성한다.|
    |HashSet(Collection<? extends E> c) |매개 변수로 받은 컬렉션 객체의 데이터를 HashSet에 담는다.|
    |HashSet(int initialCapacity)| 매개 변수로 받은 개수만큼의 데이터 저장 공간과 0.75의 로드 팩터를 갖는 객체를 생성한다.|
    |HashSet(int initialCapacity, float loadFactor)| 첫 매개 변수로 받은 개수만큼의 데이터 저장 공간과 두 번째 매개 변수로 받은 만큼의 로드팩터를 갖는 객체를 생성한다.|
- 로드팩터( load factor)? 
  - (데이터의 개수)/(저장공간)을 의미.
    - 데이터의 개수가 증가하여 로드팩터보다 커지면, 저장 공간의 크기는 증가되고 해시 재정리 작업을(rehash)을 해야만 한다.
      - 데이터가 해시 재정리 작업에 들어가면, 내부에 갖고 있는 자료 구조를 다시 생성하는 단계를 거쳐야 하므로 성능에 영향이 발생한다.
      - <b style="color:orange">로드 팩터라는 값이 클수록 공간은 넉넉해지지만, 데이터를 찾는 시간은 증가한다.</b>  
      따라서, 초기 공간 개수와 로드팩터는 데이터의 크기를 고려하여 산정하는 것이 좋다.  
      이유는 초기 크기가 (데이터의 개수)/(로드팩터)보다 클 경우에는 데이터를 쉽게 찾기 위한 해시 재정리 ㅈ가업이 발생하지 않기 때문이다.  
      따라서 대량의 데이터를 여기에 담아 처리할 때에는 초기 크기와 로드 팩터의 값을 조절해 가면서 가장 적당한 크기를 찾아야만 한다.


### HashSet의 주요 메서드를 살펴보자
- HashSet에 선언되어 있는 메서드는 그리 많지 않다.
- 부모 클래스인 AbstractSet과 AbstractCollection에 선언 및 구현되어 있는 메서드를 그대로 사용하는 경우가 많다.
- HashSet에 선언되어 있는 메서드 목록을 살펴보자.

|리턴타입|메서드 이름 및 매개 변수| 설명                                             |
|------|--------------------|------------------------------------------------|
|boolean|add(E e)           | 데이터를 추가한다.                                     |
|void|clear() | 모든 데이터를 삭제한다.                                  |
|Object|clone() | HashSet 객체를 복제한다.<br/>하지만 담겨있는 데이터들은 복제하지 않는다. |
|boolean|contains(Object o)|지정한 객체가 존재하는지를 확인한다.|
|boolean|isEmpty()|데이터가 있는지 확인한다.|
|Iterator<E>|iterator()|데이터를 꺼내기 위한 Iterator객체를 리턴한다.|
|boolean|remove(Object o)|매개 변수로 넘어온 객체를 삭제한다.|
|int|size()|데이터의 개수를 리턴한다.|

#### 예시
- 어느 회사에 직원들이 보유하고 잇는 차의 종류가 몇개나 되는지 확인해보려고 한다.  
먼저 다음과 같이 SetSample이라는 클래스를 d.collection 이라는 패키지에 만들자.  
그리고 main() 메서드에는 cars라는 배열에 직원들의 차 목록을 추가해 두었다.  
그 다음엔 getCarKinds()라는 메서드를 이용하여 몇 가지 종류의 차가 있는지 확인해 보려고 한다.
```java
package d.collection;

public class SetSample {
    public static void main(String[] args) {
        SetSample sample = new SetSample();
        String [] cars = new String[]{
                "Tico", "Sonata", "BMW", "Benz",
                "Lexus","Mustang","Grandeure",
                "The Beetle", "Mini Cooper", "i30",
                "BMW", "Lexus","Carnibal","SM5",
                "SM7", "SM3", "Tico"
        };
        System.out.println(sample.getCarKinds(cars));
    }
    public int getCarKinds(String [] cars){
        return 0;
    }
}
```
```java
package d.collection;

public class SetSample {
    public static void main(String[] args) {
        SetSample sample = new SetSample();
        String [] cars = new String[]{
                "Tico", "Sonata", "BMW", "Benz",
                "Lexus","Mustang","Grandeure",
                "The Beetle", "Mini Cooper", "i30",
                "BMW", "Lexus","Carnibal","SM5",
                "SM7", "SM3", "Tico"
        };
        System.out.println(sample.getCarKinds(cars));
    }
    public int getCarKinds(String [] cars){
        if(cars==null)return 0; // 배열이 null인지 확인 NPE방지
        if (cars.length == 1)return 1; // cars 배열의 크기가 1인지를 확인했다. 만약 배열의 크기가 1이면 확인할 필요도 없이 1이다.
        Set<String> carSet = new HashSet<String>(); // carSet 이라는 HashSet 객체를 생성한다.
        for (String car : cars){ // 생성한 carSet 객체에 cars 배열의 값들을 하나씩 담아서 중복값 없이 차이름만 남게된다.
            carSet.add(car);
        }
        return carSet.size();
    }
}
```

```java
import java.util.HashSet;
import java.util.Set;
```
- 위의 import 필요.
#### HashSet에 저장되어 있는 값을 꺼내는 예시
```java
public void printCarSet(Set<String> carSet){
    for(String temp : carSet){
        System.out.print(temp + " " );
        }
      }
```

```java
package d.collection;

public class SetSample {
    public static void main(String[] args) {
        SetSample sample = new SetSample();
        String [] cars = new String[]{
                "Tico", "Sonata", "BMW", "Benz",
                "Lexus","Mustang","Grandeure",
                "The Beetle", "Mini Cooper", "i30",
                "BMW", "Lexus","Carnibal","SM5",
                "SM7", "SM3", "Tico"
        };
        System.out.println(sample.getCarKinds(cars));
    }
    public int getCarKinds(String [] cars){
        if(cars==null)return 0; // 배열이 null인지 확인 NPE방지
        if (cars.length == 1)return 1; // cars 배열의 크기가 1인지를 확인했다. 만약 배열의 크기가 1이면 확인할 필요도 없이 1이다.
        Set<String> carSet = new HashSet<String>(); // carSet 이라는 HashSet 객체를 생성한다.
        for (String car : cars){ // 생성한 carSet 객체에 cars 배열의 값들을 하나씩 담아서 중복값 없이 차이름만 남게된다.
            carSet.add(car);
        }
        printCarSet(carSet);
        return carSet.size();
    }

    public void printCarSet(Set<String> carSet){
        for(String temp : carSet){
            System.out.print(temp + " " );
        }
    }

    public void printCarSet2(Set<String> carSet){
        Iterator<String> iterator = carSet.iterator();
        while (iterator.hasNext()){
            System.out.println();
        }
    }
}
```

- set에 저장한 순서대로 출력되지 않고, 뒤죽박죽으로 출력된 것을 볼 수 있다.
  - 순서가 중요하지 않다.
  - 찾고자 하는 해당 객체가 HashSet에 존재하는지를 확인하기 위해서는 `contains()`.
  - `HasetSet`에서 삭제하기 위해서는 `remove()`.

### Queue는 왜 필요힐까?
- LinkedList 라는 클래스가 있다.
  - 하나의 열차와 같다.
  - 배열의 중간에 있는 데이터가 지속적으로 삭제되고, 추가될 경우에는 LinkedList가 배열보다 메모리 공간 측면에서 훨씬 유리하다.
    - 배열과 같은 ArrayList와 Vector의 경우 각 위치가 정해져있고 그 위치로 데이터를 찾는다.  
    그런데 맨 앞의 값을 삭제하면, 그 뒤에 있는 값들은 하나씩 앞으로 위치를 이동해야 제대로 된 위치의 값을 가지게 된다.
    - 그에 반해 LinkedLIst는 중간에 있는 데이터를 삭제하면, 지운 데이터의 앞에 있는 데이터와 뒤에 있는 데이터를 연결하면 그만이다.  
    위치를 맞추기 위해서 값을 이동하는 단계를 거칠 필요가 없다.
  - LinkedList는 List인터페이스 뿐 아니라, Queue와 Deque 인터페이스도 구현하고 있다.
  - 즉 LinkedList자체가 List이면서도  Queue, Deque도 된다.\
  - 큐는 FIFO이다.
    - Deque는 Queue 인터페이스를 확장했기 때문에, Queue의 기능을 전부 포함한다.
      - 대신 맨 앞에 값을 넣거나 빼는 작업, 맨 뒤에 값을 넣거나 빼는 작업을 수행하는 데 용이하도록 되어 있다고 보면 된다.
  
### LinkedList를 파헤쳐보자.

- java.lang.Object
  - java.util.AbstractCollection<E>
    - java.util.AbstractList<E>
      - java.util.AbstractSequentialList<E>
        - java.util.LinkedList<E>
- ArrayList 클래스나 Vector 클래스와 상속관계는 비슷하지만, AbstractSequentialList가 부모인 것을 볼 수 있다.  
AbstractList 와 AbstractSequentialList의 차이점은 없은 add(), set(),remove() 등의 메서드에 대한 구현 내용이 상이하다는 정도다.

| 인터페이스         | 용도                                                                    |
|---------------|-----------------------------------------------------------------------|
| Serializable  | 원격으로 객체를 전송하거나, 파일에 저장할 수 있음을 지정.                                     |
| Cloneable     | Object 클래스의 clone()  메서드가 제대로 수행될 수 있음을 지정,<br/> 즉 복제가 가능한 객체임을 의미한다. |
| Iterable<E>   | 객체가 "foreach"문장을 사용할 수 있음을 지정                                         |
| Collection<E> | 여러 개의 객체를 하나의 객체에 담아 처리할 떄의 메서드 지정                                    |
| Deque<E>      | 맨 앞과 맨 뒤의 값을 용이하게 처리하는 큐와 관련된 메서드 지정                                  |
| List<E>       | 목록형 데이터를 처리하는 것과 관련된 메서드 지정                                           |
| Queue<E>      | 큐를 처리하는 것과 관련된 메서드 지정                                                 |

### LinkedList의 생성자와 주요 메서드
| 생성자                                    | 설명                                      |
|----------------------------------------|-----------------------------------------|
| LinkedList()                           | 빈 LinkedList객체를 생성                      |
| LinkedList(Collection <? extends E> c) | 매개 변수로 받은 컬렉션 객체의 데이터를 LinkedList에 담는다. |

| 리턴타입    | 메서드 이름 및 매개변수    | 설명                                           |
|---------|------------------|----------------------------------------------|
| Object  | getFirst()       | LinkedList 객체의 맨 앞에 잇는 데이터를 리턴한다.            |
| Object  | peekFirst()      | "                                            |
| Object  | peek()           | "                                            |
| Object  | element()        | "                                            |
| Object  | getLast()        | LinkedList 객체의 맨 뒤에 있는 데이터를 리턴한다.            |
| Object  | peekLast()       | "                                            |
| Object  | get(int)         | LinkedList 객체의 지정한 위치에 있는 데이터를 리턴한다.         |
| boolean | contains(Object) | 매개 변수로 넘긴 데이터가 있을 경우 true를 리턴한다.             |
| int     | indexOf(Object)  | 매개 변수로 넘긴 데이터의 위치를 앞에서부터 검색하여 리턴한다.<br/>없을경우 -1리턴 |
| int |lastIndexOf(Object)|매개 변수로 넘긴 데이터의 위치를 끝에서부터 검색하여 리턴한다.없을 경우 -1을 리턴한다.|

- LinkedList 객체의 가장 앞에 있는 데이터를 삭제/ 리턴
  - remove(), removeFirst(), poll(), pollFirst(), pop()
- LinkedList 객체의 가장 끝에 있는 데이터를 삭제하고 리턴한다.
  - pollLast(),removeLast()
- 매개 변수에 지정된 위치에 있는 데이터를 삭제하고 리턴한다.
  - remove(int)
- 매개 변수로 넘겨진 데이터와 동일한 데이터 중 앞에서부터 가장 처음에 발견된 데이터를 삭제한다.
  - remove() : 매개 변수로 넘겨진 객체와 동일한 데이트 중 앞에서부터 가장 처음에 발견된 데이털르 삭제한다.
  - removeFirstOccurrence(Object) :  앞에서부터 가장 처음에 발견된 데이털르 삭제한다.
  - removeLastOccurrence(Object) : 매개 변수로 넘겨진 객체와 동일한 데이트 중 앞에서부터 가장 처음에 발견된 데이털르 삭제한다.