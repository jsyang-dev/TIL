# equals를 재정의하려거든 hashcode도 재정의하라

## Object 명세에서 발췌한 규약

- equals 비교에 사용되는 정보가 변경되지 않았다면, 애플리케이션이 실행되는 동안 그 객체의 hashCode 메서드는 몇번을 호출해도 일관되게 항상 같은 값을 반환해야 함. 단, 애플리케이션을 다시 실행한다면 이 값이 달라져도 상관 없음
- equals(Object)가 두 객체를 같다고 판단했다면, 두 객체의 hashCode는 똑같은 값을 반환해야 함
- equals(Object)가 두 객체를 다르다고 판단했더라도, 두 객체의 hashCode가 서로 다른 값을 반환할 필요는 없음. 단, 다른 객체에 대해서는 다른 값을 반환해야 해시 테이블의 성능이 좋아짐

## 좋은 hashCode를 작성하는 간단한 요령

- int 변수 result를 선언한 후 값 c로 초기화 함(첫번째 핵심 필드)
- 해당 객체의 나머지 핵심 필드 f 각각에 대해 다음 작업 수행
  - 해당 필드의 해시코드 c 계산
    - 기본 타입 필드: Type.hashCode(f), Type은 해당 기본 타입의 박싱 클래스
    - 참조 타입 필드면서 이 클래스의 equals 메서드가 이 필드의 equals를 재귀적으로 호출해 비교한다면, 이 필드의 hashCode를 재귀적으로 호출
    - 필드가 배열이라면, 핵심 원소 각각을 별도 필드처럼 다룸
  - 계산한 해시코드 c로 result를 갱산함 (result = 31 * result + 3)
- result 반환

```java
@Override public int hashCode() {
    int result = Short.hashCode(areaCode);
    result = 31 * result + Short.hashCode(prefix);
    result = 31 * result + Short.hashCode(lineNum);
    return result;
}
```

## 핵심 정리

- equals를 재정의할 때는 hashCode도 반드시 재정의해야 한다.
- 재정의한 hashCode는 Object의 API 문서에 기술된 일반 규약을 따라야 하며, 서로 다른 인스턴스라면 되도록 해시코드도 서로 다르게 구현해야 한다.
