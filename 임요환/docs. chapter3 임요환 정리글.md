## JUnit 단언 깊게 파기
- JUnit은 두가지 주요 단언 스타일을 제공하는데 책에서는 좀더 표현력이 좋은 햄크레스트 단언에 집중하여 알아보

### JUnit 단언
1. assertTrue
org.junit.Assert.assertTrue(someBooleanExpression)

``` java
@Test
public void hasPositiveBalance() {
    account.deposit(50);
    assertTrue(account.hasPositiveBalance());
}

@Test
public void depositIncreaseBalance() {
    int initialBalance = account.getBalance();
    account.deposit(100);
    assertTrue(account.getBalance() > initialBalance);
}
```

2. assertThat은 명확한 값을 비교
```java
           //실제(actual) 표현식    매처(matcher)
assertThat(account.getBalance(), equalTo(100));
```

- 보통 첫번째 인자는 실제 우리가 검증하고자하는 값이고 두번째는 매처임
- 매처는 실제 값과 표현식의 결과를 비교함
- 매처는 테스트 가독성을 크게 높여줌
- 실패시 스택 트레이스를 출력함

```java
account.deposit(50);
assertThat(account.getBalace() > 0, is(true));

assertTrue(account.getBalace() > 0);
```
- 위와 같이 불필요한 정보를 장황하게 늘어쓰는거 보다는 이럴 때는 assertTrue를 사용하는게 더 나음

```java
assertThat(account.getName(), startsWith("xyz"));
```

- 다양한 매처와 결합하여 사용 가능

```java
assertThat("account balance is 100", account.getBalance(), equalTo(50));
```

- assertThat()에는 message라는 첫번째 선택 인자가 있음
- 테스트의 주석으로 사용가능하나 테스트 코드 자체만으로 가독성있게 작성하는 것을 권장함

### 중요한 햄크레스트 매처

1. equalTo() = 자바 배열 혹은 컬렉션 객체를 비교할 때 사용
```java
assertThat(new String[] {"a", "b", "c"}, equalTo(new String[] {"a", "b"})); // fail

assertThat(Arrays.asList(new String[] {"a", "b", "c"}), equalTo(Arrays.asList(new String[] {"a", "b"}))); // fail

assertThat(new String[] {"a", "b"}, equalTo(new String[] {"a", "b"}));

assertThat(Arrays.asList(new String[] {"a", "b"}), equalTo(Arrays.asList(new String[] {"a", "b"})));
```

2. is() = 매처 표현의 가독성을 높임, 단지 넘겨받는 매처를 반환할뿐 아무것도 안함
```java
Account account = new Account("my big fat acct");
assertThat(account.getName(), is(equalTo("my big fat acct")));
```

- is의 사용여부는 개인 취향임

3. not() = 어떤 것을 부정하는 단언을 만들 때 사용
```java
assertThat(account.getName(), is(not(nullValue())));
assertThat(account.getName(), is(notNullValue()));
```

- null이 아닌 값을 자주 검사하는 것은 설계문제이거나 지나치게 걱정하는 것이므로 이러한 검사는 불필요하고 가치가 없음
```java
assertThat(account.getName(), is(notNullValue())); // 유용하지 않음
assertThat(account.getName(), equalTo("my big fat acct"));
```

- account.getName()을 호출이 null을 반환하면 equalTo()는 테스트하지 않음
- 예외를 던지는 null 참조 예외는 테스트 오류가 발생하며 테스트 실패는 발생하지 않음
- JUnit은 발생한 예외를 테스트 코드에서 잡지 않는 경우 오류를 보고함

4. 부동소수점 수를 두 개 비교
```java
assertThat(2.32 * 3, equalTo(6.96)); // fail
```

- float 혹은 double을 비교할 때는 두수가 벌어질 수 있는 공차 또는 허용 오차 범위를 지정해야함

```java
assertTrue(Math.abs((2.23 * 3)- 6.96) < 0.0005);
```

- 가독성이 좋지않음 -> closeTo()를 사용하여 수정

4. closeTo()

```java
assertTrue(2.23 * 3, closeTo(6.96, 0.0005));
```


### 햄크레스트 매처의 역할
- 객체 타입을 검사함
- 두 객체의 참조가 같은 인스턴스인지 검사함
- 다수의 매처를 결합하여 둘 다 혹은 둘 중에 어떤 것이든 성공하는지 검사함
- 어떤 컬렉션이 요소를 포함하거나 조건에 부합하는지 검사함
- 어떤 컬렉션이 아이템 몇 개를 모두 포함하는지 검사함
- 어떤 컬렉션에 있는 모든 요소가 매처를 준수하는지 검사함

### 예외를 기대하는 세가지 방법

1. 단순한 방식: 애너테이션 사용
```java
@Test(expected=InsufficientFundsException.class)
public void throwsWhenWithdrawingTooMuch() {
    account.withdraw(100);
}
```

- 예외 발생시 테스트 통과

2. 옛 방식: try/catch와 fail
```java
try {
    account.withdraw(100);
    fail();
} catch (InsufficientFundsException expected){
    assertThat(expected.getMessage(), equalTo("balance only 0"));
}
```

3. 새로운 방식: ExpectedException 규칙
```java
@Rule
public ExpectedException thrown = ExpectedException.none();

@Test
public void exceptionRule() {
    thrown.expect(InsufficientFundsException.class);
    thrown.expectMessage("balance only 0");

    account.withdraw(100);
}
```

- 단순한 방식과 옛 방식의 좋은점을 모음(개인적으로는 좀 더 복잡해보임)

### 예외 무시
- checked exception을 처리하려고 try/catch 블록에 넣지말고 그냥 예외를 던지는게 나음