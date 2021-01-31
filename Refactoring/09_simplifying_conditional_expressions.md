# Simplifying Conditional Expressions

조건문은 코드를 이해하기 어렵게 함. 그래서 조건문을 단순하게 하는 여러가지 리팩토링 기법이 존자함

## Decompose Conditional

- 복잡한 조건문이 존재하는 경우
- if, then, else에 해당되는 부분들을 메소드로 추출(의도를 드러내는 이름의 메소드)

## Consolidate Conditional Expression

- 동일한 then 파트를 갖는 일련의 조건문이 존재하는 경우
- 하나의 조건식으로 합치고 메소드로 추출

## Consolidate Duplicate Conditional Fragments

- 동일 코드들이 조건문의 여러 분기문에 존재할 때
- 조건문 외부로 이동

## Remove Control Flag

- 일련의 boolean 표현식에 대해 제어 플래그로 동작하는 변수가 있을 때
- break나 return으로 변경

## Replace Nested Conditional with Guard Clauses

- 메소드가 명확한 실행 경로를 만들지 못하는 조건 행위를 갖는 경우
- 모든 특별한 경우(special cases)에 대해 가드절(guard clause)를 사용

## Replace Conditional with Polymorphism

- 객체의 타입에 따라 다른 행위를 갖는 조건문이 존재할 때
- 조건문에 따라 수행되는 로직들을 서부클래스의 재정의 메소드로 이동시키고 본래 메소드는 추상 메소드로 변경
- 테스트 코드: [링크](https://github.com/jsyang-dev/study-refactoring/tree/master/src/replace_conditional_with_polymorphism)
