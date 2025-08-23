-----
### 네트워크 설정 프로토콜 (NETCONF)
-----
1. 관리 서버와 피관리 네트워크 장치 사이 동작
   - 피관리 장치 설정 데이터를 검색, 셋업, 수정
   - 피관리 장치의 동작 데이터 및 통계를 질의
   - 피관리 장치에서 생성된 알림을 구독하기 위한 메세지 전송 기능

2. 관리 서버는 피관리 장치를 제어하기 위해 구조화된 XML 문서 형식의 설정 내용을 보내 피관리 장치에서 활성화
3. 원격 프로시저 호출(Remote Procedure Call, RPC) 패러다임을 사용하고, XML로 인코딩된 프로토콜 메세지는 TCP 상의 TLS(Transport Layer Security) 프로토콜과 같은 안전한 연결 지향 세션을 통해 관리 서버와 피관리 장치 사이 교환
4. NETCONF의 예
<div align="center">
<img src="https://github.com/user-attachments/assets/89b43181-7b06-4879-8057-e0e370ffb5ce">
</div>

   - 먼저 관리 서버는 피관리 장치와 보안 연결 설정 (관리 서버를 클라이언트, 피관리 서버를 서버로 지정)
   - 보안 연결이 설정되면 관리 서버와 피관리 장치는 ```<hello>``` 메세지를 교환하고, NEFCONF 명세를 보완하는 어떠한 추가 기능이 있는지 알림
   - 관리 서버와 피관리 장치 간 상호작용은 ```<rpc>```와 ```<rpc-reply>``` 메세지를 사용하는 원격 프로시저 호출 형식을 가짐
   - 이러한 메세지는 장치 설정 데이터와 동작 데이터 및 통계를 검색, 설정, 질의, 수정하고 장치의 알림을 구독하는 데 사용
   - 장치의 알림은 ```<notification>``` 메세지를 사용해 관리 장치에서 관리 서버로 서버가 요구하지 않아도 자동 전송
   - ```<close-session>``` 메세지로 세션 종료

5. 관리 서버가 피관리 장치에서 수행할 수 있는 여러 중요 NETCONF 작업
<div align="center">
<img src="https://github.com/user-attachments/assets/37d41137-00b8-401d-ba1e-41df4c7e6b40">
</div>

  - SNMP에서처럼 NETCONF에는 동작 상태 데이터를 가져오는 작업(```<get>```)과 이벤트 알림을 위한 작업(```<notification>```) 존재
  - ```<get-config>```, ```<edit-config>```, ```<lock>```, ```<unlock>``` 작업 존재는 NETCONF가 장치 설정에 특별한 강조점을 두고 있음을 보여줌
  - 기본 작업을 사용하여 장치들의 집합에서 마치 하나의 작업처럼(그룹으로) 정교한 네트워크 관리 트랜잭션 집합을 만드는 것도 가능
  - 또는 장치들을 트랜잭션 이전 상태로 되돌릴 수 있음

6. 예) 관리 서버가 피관리 장치로 보내는 XML 문서는 모든 장치 설정 및 동작 데이터를 요청하는 NETCONF ```<get>``` 명령어 : 서버는 장치 설정에 대해 알 수 있음
<div align="center">
<img src="https://github.com/user-attachments/assets/21fde37f-2bd9-40b9-b916-b998497d31d0">
</div>

   - SNMP PDU 프로토콜 메시지 형식보다 HTTP와 HTML을 훨씬 더 연상시킴
   - RPC 메세지 자체는 2 ~ 5행에 걸침
     + 2행 : 메세지 ID 값 101을 가지며 1개의 NETCONF ```<get>``` 명령 포함

<div align="center">
<img src="https://github.com/user-attachments/assets/9b1b1e0d-f94d-499a-8380-c64117e99aa0">
</div>

   - 장치의 응답 메세지는 일치하는 ID 번호 101과 4행에서 시작하여 마지막에 ```</rpc-reply>```로 끝나는, 장치의 모든 구성 데이터를 포함

7. 예) 관리 서버가 피관리 장치로 XML 문서를 보내서 Ethernet0/0이라는 인터페이스의 최대 전송 단위(Maximum Transmission Unit, MTU)를 1500바이트로 설정
<div align="center">
<img src="https://github.com/user-attachments/assets/d182f68f-f48b-4f76-a4c3-c4576437d238">
</div>

  - RPC 메세지 내용은 2 ~ 17행에 존재
  - 메세지 ID 값은 101이며 4 ~ 15행에 걸쳐 하나의 NETCONF ```<edit-config>``` 명령 기술
  - 6행 : 피관리 장치에서 실행 중인 장치 설정이 변경됨을 나타냄
  - 11행, 12행 : Ethernet0/0 인터페이스에 설정할 MTU 크기 지정
  - 피관리 장치가 자신의 설정에서 인터페이스 MTU 크기를 변경하고나면 XML 문서 내 OK 응답을 담아 관리 서버로 보냄
<div align="center">
<img src="https://github.com/user-attachments/assets/8714289f-4303-4ae1-bfda-8665a54fa3f4">
</div>

-----
### YANG
-----
1. NETCONF가 사용하는 네트워크 관리 데이터 구조, 구문 및 의미를 정확하게 표현하는 데 사용되는 데이터 모델링 언어
2. 모든 YANG 정의는 모듈에 포함되고, 장치와 해당 기능을 설명하는 XML 문서는 YANG 모듈에서 생성 할 수 있음
3. 몇 개 내장 데이터 유형을 제공하며 데이터 모델링을 하는 사람이 유효한 NETCONF 설정에 의해 충족되어야만 하는 제약 조건을 표현할 수 있도록 함
4. NETCONF 설정에서 요구되는 정확성과 일관성 제약을 충족시키는데 큰 도움
5. NETCONF 알림을 지정하는데도 사용
