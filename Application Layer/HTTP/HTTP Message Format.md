-----
### HTTP 메세지 포맷
-----
: HTTP 명세서는 HTTP 메세지 포맷을 정의하며, 요청 메세지와 응답 메세지가 존재

-----
### HTTP 요청 메세지
-----
<div align="center">
<img src="https://github.com/user-attachments/assets/85c876b5-2fce-445c-ac09-5a7cac709211">
</div>

1. ASCII 텍스트로 쓰여 있으며, 메세지가 다섯 줄로 구성되어 있고, 각 줄은 CR(Carriage Return)과 LF(Line Feed)로 구별되고, 마지막 줄에 이어서 추가 CR과 LF 존재
   - 다섯 줄로 일반적으로 구성되지만, 요청 메세지는 더 많은 줄로 구성되거나 하나의 줄이 될 수 있음

2. HTTP 요청 메세지 첫 줄은 요청 라인 (Request Line), 이후의 줄은 헤더 라인 (Header Line)
   - 요청 라인은 3개의 필드 구성 : 방식(Method) 필드, URL 필드, HTTP 버전 필드
     + 방식 필드 : GET, POST, HEAD, PUT, DELETE를 포함하는 여러 가지 값을 가질 수 있음
     + HTTP 메세지 대부분은 GET 방식 이용 (GET 방식은 브라우저가 URL 필드로 식별되는 객체를 요청할 때 사용 - 위 예제에서는 ```/somedir/page.html``` 객체 요청)
   - 헤더라인
     + ```Host: www.someSchool.edu```는 객체가 존재하는 호스트 명시
     + 💡 호스트 헤더라인이 제공하는 정보는 웹 프록시 캐시에서 필요로 함
     + ```Connection: close``` 헤더 라인 : 브라우저는 서버에게 지속 연결 사용을 원하지 않음을 명시
     + ```User-agent: ``` 헤더 라인 : 사용자 에이전트, 즉 서버에게 요청을 하는 브라우저 타입을 명시 (여기서는 Mozilla/5.0, 파이어폭스 브라우저)
       * 이 헤더 라인은 서버가 같은 객체에 대한 다른 버전을 다른 타입의 사용자에게 보낼 수 있으므로 유용
     + ```Accept-language: ``` 헤더 라인 : 사용자의 언어 버전을 의미하며, 존재하지 않으면 서버는 기본 버전을 전송 (HTTP에서 사용 가능한 컨텐츠 협상 헤더 중 하나)

<div align="center">
<img src="https://github.com/user-attachments/assets/191e6e80-a5ea-409d-9fbd-6ef7c223ac85">
</div>

3. 헤더 라인(추가 CR, LF) 이후 개체 몸체(Entity Body)가 존재
   - HTTP 클라이언트는 사용자가 폼을 채워넣을 때 POST 방식을 사용하는데, POST 메세지로 사용자는 서버에 웹 페이지를 요청하고 있으나, 웹 페이지의 특정 내용은 사용자가 폼 필드에 무엇을 입력하느냐에 따라 다름
   - 폼으로 생성한 요구가 반드시 POST 방식을 사용할 필요는 없음 : 대신 HTML 폼은 흔히 GET 방식을 사용하고 요청된 URL 입력 데이터 (폼 필드들) 전송
     * 예) GET 방식 사용, 2개의 필드를 가지며, 필드의 입력 값이 ```monkeys, bananas```라면, URL은 ```www.somesite.com/animalsearch?monkeys&bananas``` 구조
   - HEAD 방식 : HTTP 메세지로 응답하지만, 요청 객체를 보내지 않음
   - PUT 방식 : 웹 서버에 업로드할 객체를 필요로 하는 애플리케이션에 의해 사용
   - DELETE 방식 : 사용자 또는 애플리케이션이 웹 서버에 있는 객체를 지우는 것 허용

-----
### HTTP 응답 메세지
-----
<div align="center">
<img src="https://github.com/user-attachments/assets/70590e4b-34f5-4333-a6a2-770e787b6862">
</div>

1. 초기 상태 라인(Status Line), 6개의 헤더라인, 개체 몸체로 구성
   - 개체 몸체는 요청 객체를 포함
   - 상태 라인은 3개의 필드 (프로토콜 버전 필드, 상태 코드, 해당 상태 메세지) 가짐
   - 이 예에서는 서버가 HTTP/1.1 사용, 모든 것이 양호(OK)함
