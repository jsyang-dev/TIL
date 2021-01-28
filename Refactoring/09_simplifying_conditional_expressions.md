# Overview

조건문은 코드를 이해하기 어렵게 함. 그래서 조건문을 단순하게 하는 여러가지 리팩토링 기법이 존자함

## Decompose Conditional

- 조건문을 여러 조각으로 나눔
- 스위칭 로직을 실제로 일어난 구체적인 행위 로직과 분리

## Consolidate Conditional Expression

- 여러 조건 검사 로직이 있고 동일한 효과를 갖는 경우 사용

## Consolidate Duplicate Conditional Fragments

- 조건 코드의 중복을 제거

## Replace Nested Conditional with Guard Clauses & Remove Control Flag

- 하나의 종료점만 있는 코드를 작성하기 위해서는 조건문들이 동작하도록 하기 위해
- 제어 플래그를 사용함. 이 방식이 코드를 더 복잡하게 함
- 특별한 조건문을 명확하게 하고 좋지 않은 제어 플래그 제거

## Replace Conditional with Polymorphism

- 객체지향 프로그램은 절차지향에 비해 조건 행위가 적음
- 다형성으로 처리
- 다형성이 조건문 보다 좋은 이유
  - 호출하는 곳에서 조건 행위에 대해서 몰라도 됨
  - 조건문을 쉽게 확장할 수 있음(새로운 구현체 추가)
- 참고: [Github](https://github.com/jsyang-dev/study-refactoring/tree/master/src/replace_conditional_with_polymorphism)
