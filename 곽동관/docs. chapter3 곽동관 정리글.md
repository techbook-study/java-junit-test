## 요약 정리
### JUnit에서 단언이란
- 테스트에 넣을 수 있는 정적 메서드 호출
- 각 단언은 어떤 조건이 참인지 검증하는 방법
- 두가지 단언 스타일
	- 전통적인 방식의 메서드 : assertTrue
	- 햄크레스트 단언의 메서드 : assertThat
- 우리의 테스트 코드는 특정 사례에 해당 하기 때문에 검증하는 기댓값 또한 명시적으로 지정하는것이 좋다.

### 햄크레스트 매처
- 자바 배열 혹은 컬렉션 객체를 비교할 때
	- equalTo() 메서드 사용
	- ex) assertThat(new String[] {"a", "b", "c"}, equalTo(new String[] {"a", "b"})); //실패
	- null 값이 아닌 값을 검사
	- ex) assertThat(account.getName(), is(notNullValue()));

### JUnit 햄크레스트 매처를 이용할 때 할 수 있는 일
- 객체 타입을 검사한다.
- 두객체의 참조가 같은 인스턴스인지 검사한다.
- 다수의 매처를 결합하여 둘 다 혹은 둘 중에 어떤 것이든 성공하는지 검사한다.
- 어떤 컬렉션이 요소를 포함하거나 조건에 부합하는지 검사한다.
- 어떤 컬렉션이 아이템 몇 개를 모두 포함하는지 검사한다.
- 어떤 컬렉션에 있는 모든 요소가 매처를 준수하는지 검사한다.
- 등등

### 예외를 기대하는 세가지 방법
- 단순한 방식 : 애너테이션 사용
	- ex) @Test(expected=InsufficientFundsException.class)
	- expected=InsufficientFundsException.class 예외가 발생하면 테스트 통과
- 옛날 방식 : try/catch와 fail
	- ex) try { account.withdraw(100); fal();}
		- 예외가 발생하지 않으면 fail()메서드를 호출하여 강제로 실패
- 새로운 방식 : ExpectedException 규칙
	- 테스트 클래스에 ExpectedException 인스턴스를 public으로 선언하고 @Rule애너테이션 부착

### 예외 무시
- 검증된 예외를 처리하려고 테스트 코드에 try/catch블록을 넣지 마라.
	- 대신, 발생하는 예외를 다시 던져라. 



## 읽고 느낀점
흠..옛날 코드를 보면 항상 try /catch문으로 exception 처리를 하는데 그것과 TEST code에 작성하는 exception처리와는 다른가? 라는 생각이 들었고, @Test에도 많은 Exception 규칙들을 넣을 수  있다는걸 알게된 장이다.