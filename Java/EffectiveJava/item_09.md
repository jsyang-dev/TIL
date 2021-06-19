# try-finally 보다는 try-with-resources를 사용하라

- 자바 라이브러리에는 close 메서드를 호출해 직접 닫아줘야 하는 자원이 많음(InputStream, OutputStream, java.sql.Connection 등)
- 자원 닫기는 클라이언트가 놓치기 쉬워서 예측할 수 없는 성능문제를 발생시킴
- try-with-resources를 사용하려면 해당 자원이 AutoCloseable 인터페이스를 구현해야 함

## 핵심 정리

- 꼭 회수해야 하는 자원을 다룰 때는 try-finally 말고, try-with-resources를 사용하자
- try-with-resources를 사용하면 코드는 더 짧고 분명해지고, 정확하고 쉽게 자원을 회수할 수 있다

## 테스트 코드

- <https://github.com/jsyang-dev/study-effective-java/tree/master/src/item09>
