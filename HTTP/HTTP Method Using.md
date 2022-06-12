## HTTP 메서드 활용



### 1. 클라이언트에서 서버로 데이터 전송

- 쿼리 파라미터를 통한 데이터 전송
  - GET
  - 주로 정렬 필터
- 메시지 바디를 통한 데이터 전송
  - POST, PUT, PATCH
  - 회원가입, 상품 주문, 리소스 등록, 리소스 변경

- 4가지 상황
  - 정적 데이터(이미지, 정적 텍스트 문서) 조회: 쿼리 파라미터 없이 리소스 경로로 단순 조회 가능
  - 동적 데이터 조회: 검색어나 추가데이터가 있을때 쿼리 파라미터 사용, 주로 검색이나 게시판 목록에서 정렬 필터에 사용이 된다. GET은 쿼리 파라미터를 사용해 데이터 전달
  - HTML Form 데이터 전송(GET, POST만 지원): POST전송은 content-Type: application/x-www-form-urlencoded username=kim&age=20 이 디폴트이다. Multipart/form-data는 바이너리 데이터를 전송할 때 사용, 여러 파일과 폼의 내용 함께 전송 가능
  - HTTP API 데이터 전송: 서버 to 서버나 일반 데이터 전송과 유사, AJAX 나 POST, PUT, PATCH 처럼 메시지 바디를 통해 데이터 전송. Content-Type: application/json을 주로 사용.



### 2. HTTP API 설계 예시

- HTTP API - 컬렉션
  - POST 기반 등록
    - 회원 목록 /members -> GET
    - 회원 등록 /members -> POST
    - 회원 조회 /members/{id} -> GET
    - 회원 수정 /members/{id} -> PATCH, PUT, POST
    - 회원 삭제 /members/{id} -> DELETE
- POST와 PUT의 등록시 차이점
  - POST: 등록할 데이터를 넘기면 서버에서 새로 등록된 리소스 URI를 생성해주는 것 -> 컬렉션
  - PUT: 리소스 URI를 알고 등록을 해야한다. -> 스토어



- 스토어
  - 클라이언트가 관리하는 리소스 저장소
  - 클라이언트가 리소스의 URI를 알고 관리



- 컨트롤 URI
  - GET, POST만 지원하므로 제약이 있다
  - 제약 해결을 위해 동사로 된 리소스 경로 사용
  - POST의 /new, /edit, /delete가 컨트롤 URI
  - HTTP 메서드로 해결하기 애매한 경우 사용(HTML FORM)



- 참고용 좋은 URI 설계 개념
  - 문서
    - 단일 개념(파일 하나, 객체 인스턴스, 데이터 베이스)
  - 컬렉션
    - 서버가 관리하는 리소스 디렉터리
    - 서버가 리소스의 URI를 생성하고 관리
  - 스토어
    - 클라이언트가 관리하는 자원 저장소
    - 클라이언트가 리소스의 URI를 알고 관리
  - 컨트롤러, 컨트롤 URI
    - 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행
    - 동사를 직접 사용