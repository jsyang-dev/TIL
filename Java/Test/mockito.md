# Mockito

## Mockito 소개

- Mock: 진짜 객체와 비슷하게 동작하지만 프로그래머가 직접 그 객체의 행동을 관리하는 객체.
- Mockito : Mock 객체를 쉽게 만들고 관리하고 검증할 수 있는 방법을 제공한다.
- 단위 테스트에 고찰
  - [https://martinfowler.com/bliki/UnitTest.html](https://martinfowler.com/bliki/UnitTest.html)

## Mockito 시작하기

- 스프링 부트의 spring-boot-starter-test에서 자동으로 Mockito 추가해 줌
- 스프링 부트 쓰지 않는다면, 의존성 직접 추가

```groovy
testImplementation "org.mockito:mockito-core:3.1.0"
testImplementation "org.mockito:mockito-junit-jupiter:3.1.0"
```

- 다음 세 가지만 알면 Mock을 활용한 테스트를 쉽게 작성할 수 있다.
  - Mock을 만드는 방법
  - Mock이 어떻게 동작해야 하는지 관리하는 방법
  - Mock의 행동을 검증하는 방법
- Mockito 레퍼런스
  - [https://javadoc.io/doc/org.mockito/mockito-core/latest/org/mockito/Mockito.html](https://javadoc.io/doc/org.mockito/mockito-core/latest/org/mockito/Mockito.html)
  