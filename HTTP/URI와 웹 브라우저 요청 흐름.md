## URI와 웹 브라우저 요청 흐름



### 1. URI(Uniform Resource Identifier)

- Uniform: 리소스 식별하는 통일된 방식
- Resource: 자원, URI로 식별할 수 있는 모든 것(제한 없음)
- Identifier: 다른 항목과 구분하는데 필요한 정보
- URL(Uniform Resource Locator): 리소스가 있는 위치를 지정
- URN(Uniform Resource Name): 리소스에 이름을 부여
- 위치는 변할 수 있지만, 이름은 변하지 않는다
- 단, URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않았다.

문법

https://www.google.com:443/search?q=hello&hl=ko

- 프로토콜(https): 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙 ex) http, https, ftp
- 호스트명(www.google.com)
- 포트번호(443) - 접속 포트
- 패스(/search) - 리소스 경로(path), 계층적 구조
- 쿼리 파라미터(q=hello&hl=ko): key=value 형태, ?로 시작, &로 추가 가능



### 2. 웹 브라우저 요청 흐름

- HTTP 메시지 전송: TCP 3 way handshake로 연결 -> SOCKET 라이브러리를 통해 전달 -> TCP/IP 패킷 생성, HTTP 메시지 포함 -> 인터넷을 통해 서버에 전달 -> http 응답 메시지를 제작 -> 응답 메시지를 웹에 뿌려줌

