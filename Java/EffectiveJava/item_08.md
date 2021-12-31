# 아이템 8. finalizer와 cleaner 사용을 피하라

- finalizer: 예측할 수 없고, 상황에 따라 위헌할 수 있어 일반적으로 불필요
- cleaner: finalizer보다는 덜 위험하지만, 여전히 예측할 수 없고, 느리고, 일반적으로 불필요

## 문제점

- 상태를 영구적으로 수정하는 작업에서는 절대 finalizer나 cleaner에 의존해서는 안 됨
- finalizer와 cleaner는 심각한 성는 문제도 발생 시킴
- finalizer를 사용한 클래스는 finalizer 공격에 노출되어 심각한 보안 문제를 일으킬 수 있음
- 객체 생성을 막으려면 생성자에서 예외를 던지는 것만으로 충분하지만, finalizer가 있으면 그렇지 않음

## 대안

- AutoCloseable을 구현해주고, 사용 후 close 메서드를 호출하면 됨
- try-with-resources([아이템 9](item_09.md))의 사용

## 핵심 정리

- cleaner는 안전망 역할이나 중요하지 않은 네이티브 자원 회수용으로 사용하자
- 불확실성과 성능 저하에 주의해야 한다

## 테스트 코드

- <https://github.com/jsyang-dev/study-effective-java/tree/master/src/item08>
