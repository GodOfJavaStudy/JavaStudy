# 11장 귀찮은데 미리 만들어 둔걸 쓸 순 없나요?
JDK 에는 많은 클래스들과 많은 메서드들이 포함되어 있고, 이것을 상요할 때 참조하는 문서를 API라고 한다. (Application Programming Interface)
- API는 왼쪽 상단의 패키지 목록 창
- 좌측 하단의 클래스 목록 창
- 우측에 상세 설명 창  
으로 이루어져 있다.
- 좌측 하단에 있는 클래스 목록 화면에는 다음의 순서로 링크 제목이 제공된다.
  - 인터페이스 목록 ( 기울임 글자체인 italic 체로 표기)
  - 클래스 목록
  - Enum 클래스 목록
  - 예외 클래스 목록
  - 에러 Error 클래스 목록
  - 어노테이션 타입 목록 *(Annotation Types)

## 클래스 및 인터페이스의 상세 정보 화면을 살펴보자
- java.lang 패키지의 String 을 찾아보면 화면에 공통적으로 Header와 Footer가 들어간다.
- 클래스 및 인터페이스는 다음의 순서로 정보가 제공된다.
  - 패키지와 클래스/ 인터페이스 이름
  - 클래스 상속 관계 다이어그램 (Class Inheritance Diagram)
  - 직속 자식 클래스 (Direct Known Subclasses)
  - 알려진 모든 하위 인터페이스 목록(All Know Subinterfaces) 인터페이스에만 존재함
  - 알려진 모든 구현한 클래스 목록 (All Implemented Interfaces) : 클래스에만 존재함
  - 클래스 / 인터페이스의 선언 상태 (Class / Interface Declaration)
  - 클래스 / 인터페이스의 설명 ( Class / Interface Description)
  - 내부 클래스 종합 (Nested Class Summary)
  - 상수 필드 종합(Field Summary)
  - 생성자 종합(Constructor Summary)
  - 메서드 종합 (Method Summary)
  - 부모 클래스로부터 상속받은 메서드들( Methods inherited from parent)
  - 상수 필드 상세 설명 (Field Detail)
  - 생성자 상세 설명 (Constructor Detail)
  - 메서드 상세 설명 (Method Detail)

### Deprecated 표시
- 지금 사용하지 않는 것이라고 선언한 것.
- 호환성 (*Compatibility) 자바 버젼을 올릴때 마다 어떤 클래스의 메서드가 사라진다면 컴파일 오류가 나타날 수 있기 때문이다 .
- 그럼에도 불구하고 사용한다면 노트 라는 것이 두개 나타난다. 
  - APICheck 라는 클래스는 Deprecated된 API 를 사용하거나 override 한다고 알려준다.
  - -Xlint:deprecation 이라는 옵션을 주고 다시 컴파일 하라는 메시지가 나온다.
  - 실행시 warning 을 표시하며 에러가 아닌 경고를 준다.
- 