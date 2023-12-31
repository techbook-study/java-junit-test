# 3부 더 큰 설계 그림
## 깔끔한 코드로 리팩토링하기
- 리팩토링을 통한 중복의 양 최소화, 코드 구조 수정을 통한 시스템의 명확성 극대화

### 작은 리패토링
- 테스트 = 리팩토링을 위한 적절한 보호 장치

#### 리팩토링의 기회
- 빽빽하고 많은 로직을 담고 있는 메서드

#### 메서드 추출: 두 번째로 중요한 리팩토링 친구
- 리팩토링의 가장 중요한 친구 = 이름 짓기(rename)
- 코드를 안전하게 옮길 수 있는 능력(좋은 설계를 유지하며 수정, 변경, 추가)은 단위 테스트의 가장 중요한 이점임

### 메서드를 위한 더 좋은 집 찾기
- 디미테르의 법칙, 디미터의 법칙(the Law of Demeter) = 다른 객체로 전파되는 연쇄적인 메서드 호출을 피해야 함
- 임시 변수를 이용하여 값비싼 계산 값들을 캐시에 넣거나 메서드 몸체에서 변경되는 것들을 수집 할 수 있음
- 임시 변수는 코드 의도를 명확하게 할 수 있음 

### 자동 및 수동 리팩토링
- IDE가 제공하는 리팩토링 기능을 잘 활용하자
- 수동 리팩토링은 실수를 유발함

### 과한 리팩토링?
- 메서드와 반복문 추가로 성능에 좋지 않은 영향을 끼치는 것 같지만 얻는 이점도 많음

#### 보상: 명확하고 테스트 가능한 단위들
- 전체 알고리즘이 즉시 이해가능할 만큼 깔끔하게 정리됨

#### 성능 염려: 그러지 않아도 된다
- 성능이 즉시 문제되지 않으면 어설픈 최적화 노력으로 시간을 낭비하기 보다는 코드를 깔끔하게 유지하는 것이 더 나음
- 최적화된 코드는 여러 방면에서 문제 소지가 있으며 일반적으로 코드 가독성이 낮고 유지 보수 비용이 증가하고 설계 또한 유연하지 않음
- 깔끔한 설계는 성능을 위해 최적화할 때 즉시 대응 할 수 있으며 코드를 이동시킬 수 있는 유연성을 제공하고 다른 알고르짐을 적용하는 데도 수월함

### 마치며
- 단위 테스트는 기본 원칙을 깨지 않고 코드를 깔끔하게 유지해 주는 보호 장치를 제공함