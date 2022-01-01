# 아이템 10. equals는 일반 규약을 지켜 재정의하라

## 재정의가 필요하지 않은 경우

- 각 인스턴스가 본질적으로 고유함
- 인스턴스의 '논리적 동치성(logical equality)'을 검사할 일이 없음
- 상휘 클래스에서 재정의한 equals가 하위 클래스에도 딱 들어맞음
- 클래스가 private이거나 package-private이고 equals 메서드를 호출할 일이 없음

## 재정의가 필요한 경우

- 객체 식별성(두 객체가 물리적으로 같은가)이 아니라 논리적 동치성을 확인해야 함
- 상위 클래스의 equals가 논리적 동치성을 비교하도록 재정의되지 않았을 경우(주로 값 클래스들이 여기에 해당됨)
  - 값 클래스라 해도, 값이 같은 인스턴스가 둘 이상 만들어지지 않음을 보장하는 인스턴스 통제 클래스([아이템 1](item_01.md))라면 재정의가 필요 없음
  - Enum([아이템 34](item_34.md))도 여기에 해당됨

## equals 메서드 재정의 일반 규약

- 반사성: null이 아닌 모든 참조 값 x에 대해, x.equals(x)는 true다
- 대칭성: null이 아닌 모든 참조 값 x, y에 대해, x.equals(y)가 true면 y.equals(x)도 true다
- 추이성: null이 아닌 모든 참조 값 x, y, z에 대해, x.equals(y)가 truerh y.equals(z)도 true면 x.equals(z)도 true다
- 일관성: null이 아닌 모든 참조 값 x, y에 대해, x.equals(y)를 반복해서 호출하면 항상 true를 반환하거나 항상 false를 반환한다
  - eqals의 판단에 신뢰할 수 없는 자원이 끼어들게 해서는 안됨
- null-아님: null이 아닌 모든 참조 값 x에 대해, x.equals(null)은 false다

## 양질의 equals 메서드 구현 방법

- == 연산자를 사용해 입력이 자기 자신의 참조인지 확인
- instanceof 연산자로 입력이 올바른 타입인지 확인
- 입력을 올바늘 타입으로 형변환
- 입력 객체와 자기 자신의 대응되는 '핵심'필드들이 모두 일지하는지 하나씩 검사
  - float와 double을 제외한 기본 타입 필드: == 연산자로 비교
  - 참조 타입: 각각의 equals 메서드
  - float와 double 필드: Float.compare(float, float), Double.compare(double, double)로 비교
- equals를 다 구현했다면 세 가지만 자문해보자, 대칭적인가? 추이성이 있는가? 일관적인가?(단위 테스트 작성)

## 주의 사항

- equals를 재정의할 땐 hashcode도 반드시 재정의하자([아이템 11](item_11.md))
- 너무 복잡하게 해결하려 들지 말자
- Object 외의 타입을 매개변수로 받는 equals 메서드는 선언하지 말자

## 핵심 정리

- 꼭 필요한 경우가 아니면 equals를 재정의 하지 말자
- 재정의해야 할 때는 그 클래스의 핵심 필드 모두를 빠짐없이, 다섯가지 규약을 확실히 지켜가면 비교해야 한다

## 테스트 코드

- <https://github.com/jsyang-dev/study-effective-java/tree/master/src/item10>
