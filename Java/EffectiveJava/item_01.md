# 아이템 1. 생성자 대신 정적 팩터리 메서드를 고려하라

- 클라이언트가 클래스의 인스턴스를 얻는 전통적인 수단은 public 생성자이지만, 정적 팩터리 매서드(static factory method)를 제공하는 방법도 있다

```java
// java.lang.Boolean
public static Boolean valueOf(boolean b) {
    return (b ? TRUE : FALSE);
}
```

## 장점 1: 이름을 가질 수 있다

- 생성자의 매개변수와 생성자 자체로는 반환될 객체의 특성을 설명하기 어려움
- 정적 팩터리 메서드는 이름만 잘 지으면 반환될 객체의 특성을 쉽게 묘사 가능

```java
// 생성자: 반환될 객체의 특성 불분명
BigInteger bigInteger1 = new BigInteger(3, 1, new Random());

// 정적 팩터리 메소드: 소수인 BigInteger를 반환 한다는 의미 설명
BigInteger bigInteger2 = BigInteger.probablePrime(3, new Random());
```

## 장점 2: 호출될 때마다 인스턴스를 새로 생성하지는 않아도 된다

- 불변 클래스([아이템 17](item_17.md))는 인스턴스를 미리 만들어 놓거나 새로 생성한 인스턴스를 캐싱하여 재활요하는 식으로 불필요한 개체 생성 회피 가능
- 반복되는 요청에 같은 객체를 반환하는 식으로 정적 팩터리 방식의 클래스는 언제 어느 인스턴스를 살아 있게 할지를 철저히 통제 가능
- 인스턴스를 통제하는 이유
  - 클래스를 싱글턴([아이템 3](item_03.md))으로 만들 수도, 인스턴스화 불가(아이템 4)로 만들 수도 있음
  - 불변 값 클래스([아이템 17](item_17.md))에서 동치인 인스턴스가 단 하나뿐임을 보장 가능
  - 열거 타입([아이템 34](item_34.md))은 인스턴스가 하나만 만들어짐을 보장함

## 장점 3: 반환 타입의 하위 타입 객체를 반환할 수 있는 능력이 있다

- 반환할 객체의 클래스를 자유롭게 선택할 수 있게 하는 '엄청난 유연성'을 선물함
- 이를 응용하면 구현 클래스를 공개하지 않고도 그 객체를 반환할 수 있어 API를 작게 유지 가능
- 인터페이스 기반 프레임워크([아이템 20](item_20.md))를 만드는 핵심 기술
- 정적 팩터리 메서드로 얻은 객체를 인터페이스만으로 다루는 것이 가능함([아이템 64](item_64.md))

## 장점 4: 입력 매개변수에 따라 매번 다른 클래스의 객체를 반환할 수 있다

- 반환 타입의 하위 타입이기만 하면 어떤 클래스든 반환 가능

```java
public static <E extends Enum<E>> EnumSet<E> of(E e) {
    EnumSet<E> result = noneOf(e.getDeclaringClass());
    result.add(e);
    return result;
}

public static <E extends Enum<E>> EnumSet<E> noneOf(Class<E> elementType) {
    Enum<?>[] universe = getUniverse(elementType);
    if (universe == null)
        throw new ClassCastException(elementType + " not an enum");

    if (universe.length <= 64)
        return new RegularEnumSet<>(elementType, universe);
    else
        return new JumboEnumSet<>(elementType, universe);
}
```

## 장점 5: 정적 패팩터리 메서드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다

- 이런 유연함은 서비스 제공자 프레임워크를 만드는 근간이 됨
- 서비스제공자 프레임워크의 핵심 컴포넌트
  - 서비스 인터페이스(service interface): 구현체의 동작 정의
  - 제공자 등록 API(provider registration API): 제공자가 구현체를 등록할 때 사용
  - 서비스 접근 API(service access API): 클라이언트가 서비스의 인스턴스를 얻을 때 사용
  - 서비스 제공자 인터페이스(service provider interface): 서비스 인터페이스의 인스턴스를 생성하는 팩터리 객체 설명

## 단점 1: 상속을 하려면 public이나 protected 생성자가 필요하니 정적 팩터리 메서드만 제공하면 하위 클래스를 만들 수 없다

- 상속보다 컴포지션을 사용([아이템 18](item_18.md))하도록 유도하고 불변 타입([아이템 17](item_17.md))으로 만들려면 이 제약을 지켜야 한다는 점에서 오히려 장점으로 받아들일 수 있음

## 단점 2: 정적 팩터리 메서드는 프로그래머가 찾기 어렵다

- 생성자처럼 API 설명에 명확하게 드러나지 않으니 사용자는 정적 팩터리 메서드 방식 클래스를 인스턴스화할 방법을 알아내야 함
- 정적 팩터리 메서드에 흔히 사용하는 명명 방식
  - from: 매개변수를 하나 받아서 해당 타입의 인스턴스 반환
    - `Date d = Date.from(instance);`
  - of: 여러 매개변수를 받아 적합한 타입의 힌스턴스 반환
    - `Set<Rank> faceCards = EnumSet.of;`
  - valueOf: from과 of의 더 상세한 버전
    - `BigInteger prime = BigInteger.valueOf(Integer.MAX_VALUE);`
  - instance, getInstance: (매개변수를 받는다면) 매개변수로 명시한 인스턴스를 반환하지만, 같은 인스턴스임을 보장하지 않음
    - `StackWalker luke = StackWalker.getInstance(option);`
  - create, newInstance: instance 혹은 getInstance와 같지만, 매번 새로운 인스턴스를 생성해 반환함을 보장
    - `Object newArray = Array.newInstance(classObject, arrayLen);`
  - getType: getInstance 와 같으나, 생성할 클래스가 아닌 다른 클래스에 팩터리 메서드를 정의할 때 사용
    - `FileStore fs = Files.getFileStore(path);`
  - newType: newInstance와 같으나, 생성할 클래스가 아닌 다른 클래스에 팩터리 메서드를 정의할 때 사용
    - `BufferedReader br = Files.newBufferedReader(path);`
  - type: getType과 newType의 간결한 버전
    - `List<Complaint> litany = Collections.list(legacyLitany);`

## 핵심 정리

- 정적 팩터리 메서드와 public 생성자는 각자의 쓰임새가 있으니 상대적인 장단점을 이해하고 사용하는 것이 좋다
- 정적 팩터리를 사용하는 게 유리한 경우가 더 많으므로 무작정 public 생성자를 제공하는 습관은 고치자

## 테스트 코드

- <https://github.com/jsyang-dev/study-effective-java/tree/master/src/item01>
