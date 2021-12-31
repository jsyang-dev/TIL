# 아이템 5. 자원을 직접 명시하지 말고 의존 객체 주입을 사용하라

- 인스턴스를 생성할 때 생성자에 필요한 자원을 넘겨주는 방식
- 사용하는 자원에 따라 동작이 달라지는 클래스에는 정적 유틸리티 클래스나 싱글턴 방식이 적합하지 않음
- 불변([아이템 17](item_17.md))을 보장하여 여러 클라이언트가 의존 객체들을 안심하고 공유할 수 있음
- 스프링(Spring) 같은 의존 객체 주입 프레임워크를 사용하면 어질러짐을 해소할 수 있음

```java
public class SpellChecker {
    private final Lexicon dictionary;

    public SpellChecker(Lexicon dictionary) {
        this. dictionary = Object.requireNonNull(dictionary);
    }

    public boolean isValid(String word) { ... }
    public List<String> suggestions(String typo) { ... }
}
```

## 핵심 정리

- 클래스가 내부적으로 하나 이상의 자원에 의존하고, 그 자원이 클래스 동작에 영향을 준다면 싱글턴과 정적 유틸리티 클래스는 사용하지 않는 것이 좋다
- 대신 필요한 자원을 생성자에 넘겨주면 클래스의 유연성, 재사용성, 테스트 용이성을 기막히게 개선해준다
