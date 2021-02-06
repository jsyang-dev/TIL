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

### URI

- URI(Uniform Resource Identifier)
  - Uniform: 리소스 식별하는 통일된 방식
  - Resource: 자원, URI로 식별할 수 있는 모든 것(제한 없음)
  - Identifier: 다른 항목과 구분하는데 필요한 정보
  - URL, URN을 포함한 개념
  - 전체 문법: scheme://[userinfo@]host[:port][/path][?query][#fragment]
- URL(Uniform Resource Locator)
  - 리소스가 있는 위치를 지정
- URN(Uniform Resource Name)
  - 리스소에 이름을 부여
  - 예: urn:isbn:8960777331

### HTTP 기본

- HTTP 역사
  - HTTP/0.9 1991년: GET 메서드만 지원, HTTP 헤더X
  - HTTP/1.0 1996년: 메서드, 헤더 추가
  - HTTP/1.1 1997년: 가장 많이 사용, 우리에게 가장 중요한 버전
  - HTTP/2 2015년: 성능 개선
  - HTTP/3 진행중: TCP 대신에 UDP 사용, 성능 개선
- HTTP 특징
  - 클라이언트 서버 구조
    - Request/Response 구조
    - 클라이언트는 서버에 요청을 보내고 응답을 대기
    - 서버가 요청에 대한 결과를 만들어서 응답
  - 무상태 프로토콜(stateless)
    - 서버가 클라이언트의 상태를 보존하지 않음
    - 장점: 서버 확장성 높음(Scale-out)
    - 단점: 클라이언트가 추가 데이터 전송
  - 비연결성(connectionless)
    - HTTP는 기본이 연결을 유지하지 않는 모델
    - 장점: 서버 자원을 매우 효율적으로 사용할 수 있음
    - 단점: TCP/IP 연결을 새로 맺어야 함
  - HTTP 메시지
    - 시작라인
      - 요청 메시지: method SP(공백) request-target SP HTTP-version CRLF(엔터)
        - GET /search?q=hello&hl=ko HTTP/1.1
      - 응답 메시지: HTTP-version SP status-code SP reason-phrase CRLF
        - HTTP/1.1 200 OK
    - HTTP 헤더
      - HTTP 전송에 필요한 모든 부가정보
      - field-name ":" OWS field-value OWS (OWS:띄어쓰기 허용)
        - Host: www.google.com
        - Content-Type: text/html;charset=UTF-8
        - Content-Length: 3423
    - HTTP 메시지 바디
      - 실제 전송할 데이터
      - HTML 문서, 이미지, 영상, JSON 등등 byte로 표현할 수 있는 모든 데이터 전송 가능
  - 단순함, 확장 가능

### HTTP 메서드

### HTTP 메서드 활용

### HTTP 상태 코드

### HTTP 헤더
