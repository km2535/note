- HTTP는 Hyper Transfer Protocol의 약자로 웹 상에서 정보를 주고 받을 수 있는 프로토콜을 의미 
- 클라이언트 요청과 서버 응답이라는 통신 모델 사용


## Connectionless & Stateless 프로토콜
### Connectionless
- 서버에 연결하고, 요청해서 응답을 받으면 연결을 지속하지 않음
- 접속 유지는 최소한으로 유지, 더 많은 유저의 요청 처리
### Stateless
- HTTP는 cookie 등을 이용해 클라이언트의 이전 상태를 기억함
- Stateless 특성에 따라 과거 상태를 가지고 있지 않기 때문에 많은 양의 요청을 빠르게 처리하는 반면, Stateless 프로토콜은 서버가 많은 클라이언트의 상태를 기억해야 하기 때문에 서버 리소스가 부담.


## HTTP 메시지 타입
- HTTP메시지는 서버와 클라이언트 간에 데이터가 교환되는 방식
- 요청
	- 클라이언트가 서버로 전달해서 서버의 액션이 일어나게끔 하는 메시지
- 응답
	- 요청에 대한 서버의 답변

### HTTP 요청 메서드
- 클라이언트에서 요청하는 데이터에 특정 동작을 수행하고 싶을 때 설정
- GET
	- 존재하는 자원에 대한 요청
	- URI로 지정한 정보를 도출
- POST
	- 새로운 자원을 생성
	- 폼에 입력한 데이터를 송신
- PUT
	- 존재하는 자원에 대한 변경
	- URI로 지정한 서버의 파일을 치환
- DELET
	- 존재하는 자원에 대한 삭제
	- URI로 지정한 서버의 파일을 삭제
- HEAD
	- 서버 헤더 정보를 획득
	- GET과 비슷
- OPTION
	- CORS에서 사용


### 상태코드
- HTTP 상태코드
	- 서버에서 설정해주는 응답에 대한 정보
- 2XX
	- 200번대의 상태 코드는 대부분 성공
- 3XX
	- 300번대의 상태코드는 대부분 클라이언트가 이전 주소로 데이터를 요청하여 서버에서 새 URL로 리다이렉트를 유도하는 경우
- 4XX
	- 400번대 상태코드는 대부분 클라이언트의 코드가 잘못된 경우
	- 유효하지 않는 자원을 요청했거나, 요청이나 권한이 잘 못된 경우
- 5XX
	- 500번대 상태 코드는 서버 쪽에서 오류

### HTTP Header의 속성
- General Header
	- 요청과 응답에 모두 적용, 데이터와 관련 없는 헤더
- Request Header
	- 요청에 대한 자세한 정보를 포함하는 헤더를 의미
	- HOST User-Agent, Cookie 정보를 포함
- Response Header
	- 서버 자체에 대한 정보, 응답에 대한 부가적인 정보를 포함하는 헤더를 의미
	- Server, Allow, ETag, Access-Control-Allow-Origin 정보를 포함
- Entity Header 
	- 컨텐츠의 길이나 MIME 타입과 같이 엔티티 바디에 대한 자세한 정보를 포함하는  헤더
	- Content-Type, Content-Length 처럼 본문 리소스 관련 정보를 포함





























