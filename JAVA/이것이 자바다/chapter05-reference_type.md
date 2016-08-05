## 참조타입
Chapter05 - p138 ~ p180

### 데이터 타입 분류
- 기본 타입(primitive type) - 정수, 실수 문자, 논리 리터럴
- 참조 타입(reference type) - 배열, 열거, 클래스, 인터페이스 - 객체(Object)의 번지를 참조하는 타입

### 메모리 사용 영역
java.exe로 JVM이 시작되면 JVM은 운영체제에서 할당받은 메모리 영역(Runtime Data Area)을 다음과 같이 세부 영역으로 구분해서 사용한다.

- 메소드(Method) 영역  
메소드 영역에는 코드에서 사용되는 클래스(~.class)들을 클래스 로더로 읽어 클래스별로 런타임 상수풀(runtime constant pool),  필드(field) 데이터, 메소드(method) 데이터, 메소드 코드, 생성자(constructor) 코드 등을 분류해서 저장한다. 메소드 영역은 JVM이 시작할 때 생성되고 모든 스레드가 공유하는 영역이다.

- 힙(heap) 영역  
객체와 배열이 생성되는 영역으로 JVM 스택 영역의 변수나 다른 객체의 필드에서 참조한다. 참조하는 변수나 필드가 없다면 GC를 실행한다.

- JVM 스택(Stack) 영역  
JVM 스택 영역은 각 스레드마다 하나씩 존재하며 스레드가 시작될 때 할당된다. 초기에는 main 스레드만 존재. 메소드 호출 시 프레임(Frame)을 추가(push) 하고 종료되면 제거(pop)한다.
프레임 내부에 있는 로컬 변수 스택에 기본 타입 변수와 참조 타입 변수가 추가되거나 제거된다. 변수에 값이 저장될때 추가되고 블록을 벗어나면 제거된다.

### 배열 복사
배열의 크기를 변경할 수 없기때문에 변경하려면 새로운 배열을 만든후 이전 배열을 복사해야 한다.

- for문
```java
for(int i=0; i<oldIntArray.length; i++) {
  newIntArray[i] = oldIntArray[i];
}
```

- System.arraycopy() 메소드
```java
// 원본 배열, 원본 시작 인덱스, 복사할 배열, 복사 시작 인덱스, 복사할 개수
System.arraycopy(src, srcPos, dest, destPos, length);
```

### 열거 타입
열거 타입(enumeration type) - 한정된 값을 갖는 타입 (ex: 요일, 계절등)

- 열거 타입 선언  
PascalCase로 .java 파일 생성 (ex: Week.java, MemberGrade.java)

- 열거 상수 선언  
관례적으로 모두 대문자 사용, 띄어쓰기는 언더바
```java
public enum Week { MONDAY, TUESDAY, WEDNESDAY... }
```
