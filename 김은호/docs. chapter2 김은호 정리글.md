## 정리
- [길벗 source](https://github.com/gilbutITbook/006814)를 토대로 commit 내용을 정리해 커밋 기록을 정리글로 남기려 합니다. 


1. code. chapter2 - enum: Weight을 만들어라

2. code. chapter2 - enum: Bool을 만들어라

3. code. chapter2 - 문제과 정답을 만들어라
    - abstract class: Question
    - class: Answer
    - class: BooleanQuestion
    - class: PercentileQuestion

4. mod. chapter2 - package: 모든 파일의 위치를 questionnaire로 이동하라
    - chapter01 -> questionnaire 변경
    - 입력한 모든 파일 questionnaire 패키지

5. code. chapter2 - Criteria와 Criterion을 만들어라
    - class: Criteria implements Iterable<Criterion>
    - class: Criterion implements Scoreable

6. code. chapter2 - Person을 만들어라

7. code. chapter2 - Profile을 만들어라

8. test. chapter2 - mustMatch 기준을 충족못하면 답변은 false를 리턴하라
    - profile answer = qeustion -> false
    - criteria answer = question -> true
    - criterion -> criteria answer, MustMatch

9. test. chapter2 - dontcare_기준을_충족못해도_답변은_true를 리턴하라
    - profile answer = qeustion -> false
    - criteria answer = question -> true
    - criterion -> criteria answer, DontCare

10. test. chapter2 - 리팩터링: 공통으로 사용되는 Profile, Question, Criteria를 @beforeEach로 표현하라
    - 상호 코드에  영향을 줄 수 있는 static 작성을 지양합니다.