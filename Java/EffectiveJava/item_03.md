# private 생성자나 열거 타입으로 싱글턴임을 보증하라

싱글턴(ingleton)이란 인스턴스를 오직 하나만 생성할 수 있는 클래스를 말한다.
클래스를 싱글턴으로 만들면 이를 사용하는 클라이언트를 테스트하기가 어려워질 수 있다.

## public static final 필드

- private 생성자는 public static final 필드를 초기화할 때 한 번만 호출됨
- public이나 protected 생성자가 없으므로 초기화될 때 만들어진 인스턴스가 전체 시스템에서 하나뿐임이 보장됨
- 장점  
  - 해당 클래스가 싱글턴임이 API에 명백히 드러남
  - 간결함

## 정적 팩터리

- 정적 팩터리 메서드에서 항상 같은 객체의 참조를 반환하므로 인스턴스는 한개만 생성됨
- 장점
  - API를 바꾸지 않고도 싱글턴이 아니게 변경 가능
  - 정적 팩터리를 제네릭 싱글턴 팩터리로 만들 수 있음([아이템 20](item_20.md))
  - 정적 팩터리의 메서드 참조를 공급자(supplier)로 사용 가능([아이템 43](item_43.md), [아이템 44](item_44.md))

## 직렬화(Serialization)

- public static final 필드나 정적 팩터리 방식으로 만든 싱글턴 클래스를 역직렬화할 때 새로운 인스턴스가 생길 수 있음
- 모든 인스턴스 필드를 일시적(transient)이라고 선언하고 readResolve 메서드를 제공하면 방지 가능([아이템 89](item_89.md))

```java
private Object readResolve() {
    return INSTANCE;
}
```

## 열거 타입(Enum)

- public static final 필드 방식과 비슷하지만, 더 간결하고, 추가 노력 없이 직렬화 가능
- 복잡한 직렬화 상황이나 리플렉션 공격에서도 제2의 인스턴스가 생기는 일을 완벽히 막아줌
- 대부분의 상황에서 원소가 하나뿐인 열거 타입이 싱글턴을 만드는 가장 좋은 방법

## 테스트 코드

- [https://github.com/jsyang-dev/study-effective-java/tree/master/src/item03](https://github.com/jsyang-dev/study-effective-java/tree/master/src/item03)
