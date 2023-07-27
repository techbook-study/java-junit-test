## 테스트 조직
### AAA로 테스트 일관성 유지
- 준비(Arrange) = 테스트 코드를 실행하기 전에 시스템에 적절한 상태에 있는지 확인
- 실행(Act) = 테스트 코드를 실행
- 단언(Assert) = 실행한 코드가 기대한 대로 동작하는지 확인
- 사후(After) = 테스트를 실행할 떄 어떤 자원을 할당했다면 잘 정리되었는지 확인해야함, 때에 따라 필요한 4번째 단계

### 동작 테스트 vs 메서드 테스트
- 단위 테스트를 작성할 때는 전체적인 시각에서 작성해야함
- 개별 메서드를 테스트하는 것이 아니라 클래스의 종합적인 동작을 테스트해야함

### 테스트와 프로덕션 코드의 관계
- 테스트는 프로덕션 코드와 분리해야됨

### 집중적인 단일 목적 테스트의 가치
- 다수의 케이스를 별도의 JUnit 테스트 메서드로 분리, 각각에는 검증하는 동작을 표현하는 이름을 붙임
- 테스트 분리
    - 단언이 실패했을 시 실패한 테스트의 이름이 나오기 때문에 문제 파악이 쉬움
    - 실패한 테스트를 해독하는 데 피룡한 시간을 줄일 수 있음
    - 모든 케이스가 실행되었음을 보장함

### 문서로서의 테스트
- 단위 테스트트 클래스에 대한 지속적이고 믿을 수 있는 문서 역할을 함

#### 일관성 있는 이름으로 테스트를 문서화 해야함
- doingSomethingOperationGeneratesSomeResult(어떤 동작을 하면 어떤 결과가 나온다)
- someResultOccursUnderSomeCondition(어떤 결과는 어떤 조건에서 발생한다)
- 행위주도개발(BDD, Behavior-Driven Development)에서 말하는 given-when-then 같은 양식도 있음
- givenSomeContextWhenDoingSomeBehaviorThenSomeResultsOccurs(주어진 조건에서 어떤 일을 하면 어떤 결과가 나온다)
- whenDoingSomeBehaviorThenSomeResultsOccurs(어떤 일을 하면 어떤 결과가 나온다)

#### 테스트를 의미 있게 만들기
- 테스트 이름 개선
- 지역 변수 이름 개선
- 의미 있는 상수 도입
- 햄크레스트 단언 사용
- 커다란 테스트를 작게 나누어 집중적인 테스트 만들기
- 테스트 군더더기들을 도우미 메서드와 @Before 메서드로 이동하기

### @Before와 @After(공통 초기화 정리) 더 알기 -> JUnit5 @BeforeEach, @AfterEach
- @Before 메서드를 사용하여 중복된 초기화 코드를 제거함 = setup 메서드
- @After 메서드는 테스트의 부산물들을 정리함 = cleanup 메서드
- @BeforeClass, @AfterClass -> JUnit5 @BeforeAll, @AfterAll -> 해당 클래스의 테스트에서 한번만 실행됨(static)

### 녹색이 좋다: 테스트를 의미 있게 유지
- 실패하는 테스트가 있다면 더 늘리지 말고 곧바로 고쳐서 모든 테스트가 항상 통과하도록 해야함
- 단위 테스트를 빠르게하는 방법으로 목 객체를 활용하는 법이 있음
- @Ignore -> JUnit5 @Disabled 를 이용해 문제가 있는 테스트에 집중하고 다른 실패 테스트는 주석처리를 할 수 있음