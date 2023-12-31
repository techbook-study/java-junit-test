## Right-BICEP: 무엇을 테스트할 것인가?
- 무엇을 테스트하는 것이 중요한지에 대한 지침

### [Right]-BICEP: 결과가 올바른가?
- 테스트 코드는 무엇보다도 기대한 결과를 산출할는지 검증할 수 있어야 함

### Right-[B]ICEP: 경계 조건(boundary conditions)은 맞는가?
- 경계 조건 예시
    - 모호하고 일관성 없는 입력 값, 특수 문자가 포함된 파일 이름 등
    - 잘못된 양식의 데이터, 최상위 도메인이 빠진 이메일 주소
    - 수치적 오버플로를 일으키는 계산
    - 비거나 빠진 값, 0, 0.0, "", null 등
    - 이상적인 기댓값을 훨씬 벗어나는 값, 150세의 나이
    - 교실의 당번표처럼 중복을 허용해서는 안되는 목록에 중복 값이 있는 경우
    - 정렬이 안 된 정렬 리스트 혹은 그 반대
    - 시간 순이 맞지 않는 경우
### 경계 조건에서는 CORRECT를 기억하라
- Conformance(준수) : 값이 기대한 양식을 준수하고 있는가?
- Ordering(순서) : 값의 집합이 적절하게 정렬되거나 정렬되지 않았나?
- Range(범위) : 이성적인 최솟값과 최댓값 안에 있는가?
- Reference(참조) : 코드 자체에서 통제할 수 없는 어떤 외부 참조를 포함하고 있는가?
- Existence(존재) : 값이 존재하거나(널이 아니거나, 0이 아니거나, 집합에 존재하는가 등)?
- Cardinality(기수) : 정확히 충분한 값들이 있는가?
- Time(절대적 혹은 상대적 시간) : 모든 것이 순서대로 일어나는가? 정확한 시간에? 정시에?

### Right-B[I]CEP: 역 관계(inverse relationship)를 검사할 수 있는가?
- 데이터베이스에 데이터를 넣는 코드가 있다면 테스트에서 직접적인 JDBC 쿼리를 해보는 것도 하나의 방법임

### Right-BI[C]EP: 다른 수단을 활용하여 교차 검사(cross-check)할 수 있는가?
- 느리거나 유연하지 않은 패배자 해법들은 교차 검사할 떄 활용할 수 있음
- 클래스의 서로 다른 조각 데이터를 사용하여 모든 데이터가 합산되는지 확인해 보는 것

### Right-BIC[E]P: 오류 조건(error conditions)을 강제로 일어나게 할 수 있는가?
- 디스크 풀, 네트워크 선 끊김 등에 대해 대비 할 수 있도록 테스트 오류를 강제로 발생 시킬 수 있어야 함
- 환경적인 제약 사항들
    - 메모리가 가득 찰 때
    - 디스크 공간이 가득 찰 때
    - 벽시계 시간에 관한 문제들(클라이언트와 서버의 시간이 다를 때 생기는 문제)
    - 네트워크 가용성 및 오류들
    - 시스템 로드
    - 제한된 색상 팔레트
    - 매우 높거나 낮은 비디오 해상도
- 좋은 단위 테스트는 단지 코드에 존재하는 로직 전체에 대한 커버리지를 달성하는게 아님
- 가장 끔찍한 결함들은 종종 전혀 예쌍하지 못한 곳에서 나옴

### Right-BICE[P]: 성능 조건(performance characteristics)은 기준에 부합하는가?
- 실제로 병목 지점(bottleneck)이 어디인지 증명되기 전까지는 미리 짐작하여 코드를 난도질하지 마라
- 추측만으로 성능 문제에 바로 대응하기 보다는 단위 테스트를 설계하여 진짜 문제를 파악해야 함
- JMeter, JunitPerf 같은 도구를 사용해도 됨

### 마치며
- Right-BICEP 암기법을 활용하여 행복 경로, 경계 조건과 오류 조건을 다루는 테스트를 작성해야 함
- 결과를 교차로 검사하고 역 관계를 살펴보며 테스트 코드의 유효성을 강화할 수 있음
- 언제 코드의 성능을 보는 것이 유용하진도 알음