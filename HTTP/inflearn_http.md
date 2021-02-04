# 모든 개발자를 위한 HTTP 웹 기본 지식

## 강의 정보

- 사이트: [인프런](https://www.inflearn.com/)
- 강사: 김영한
- 강의 링크: [모든 개발자를 위한 HTTP 웹 기본 지식](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC)

## 강의 내용

### 인터넷 네트워크

- IP(Internet Protocol)
  - 지정한 IP 주소(IP Address)에 데이터 전달
  - 패킷(Packet)이라는 통신 단위로 데이터 전달
  - IP 프로토콜의 한계: 비연결성, 비신뢰성, 프로그램 구분
- TCP(Transmission Control Protocol)
  - 연결지향: TCP 3 Way-Handshake (가상연결)
    - ![TCP 3 Way-Handshake](https://user-images.githubusercontent.com/35869083/106898702-dcc9b180-6737-11eb-9347-d174e7d24c5f.png)
  - 데이터 전달 보증
  - 순서 보장
  - 신뢰할 수 있는 프로토콜
- UDP(User Datagram Protocol)
  - 데이터 전달 및 순서가 보장도지 않지만, 단순하고 빠름
  - IP와 거의 비슷 + PORT, 체크섬 정도만 추가
  - 애플리케이션에서 추가 작업 필요
- PORT
  - 같은 IP 내에서 프로세스 구분
  - 0 ~ 65535 할당 가능
  - 0 ~ 1024: 잘 알려진 포트, 사용하지 않는 것이 좋음
- DNS(Domain Name System))
  - 도메인 명을 IP 주소로 변환

### URI와 웹 브라우저 요청 흐름

### HTTP 기본

### HTTP 메서드

### HTTP 메서드 활용

### HTTP 상태 코드

### HTTP 헤더
