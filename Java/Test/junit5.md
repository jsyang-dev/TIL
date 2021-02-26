# 더 자바, 애플리케이션을 테스트하는 다양한 방법

## junit-platform.properties

- JUnit 설정 파일로, 클래스패스 루트 (src/test/resources/)에 넣어두면 적용된다.
- 테스트 인스턴스 라이프사이클 설정
  - junit.jupiter.testinstance.lifecycle.default = per_class
- 확장팩 자동 감지 기능
  - junit.jupiter.extensions.autodetection.enabled = true
- @Disabled 무시하고 실행하기
  - junit.jupiter.conditions.deactivate = org.junit.*DisabledCondition
- 테스트 이름 표기 전략 설정
  - junit.jupiter.displayname.generator.default = org.junit.jupiter.api.DisplayNameGenerator$ReplaceUnderscores

## 확장 모델

- JUnit 4의 확장 모델은 @RunWith(Runner), TestRule, MethodRule.
- JUnit 5의 확장 모델은 단 하나, Extension.
- 확장팩 등록 방법
  - 선언적인 등록 @ExtendWith
  - 프로그래밍 등록 @RegisterExtension
  - 자동 등록 자바 ServiceLoader 이용
- 확장팩 만드는 방법
  - 테스트 실행 조건
  - 테스트 인스턴스 팩토리
  - 테스트 인스턴스 후-처리기
  - 테스트 매개변수 리졸버
  - 테스트 라이프사이클 콜백
  - 예외 처리
- 참고
  - [https://junit.org/junit5/docs/current/user-guide/#extensions](https://junit.org/junit5/docs/current/user-guide/#extensions)
  