-----
### 공개 키 인증
-----
1. 어떤 공개키가 특정 통신 개체에 속한다는 것을 보증하는 것
2. 공개키 인증은 IPSec과 TLS를 포함한 많은 대중적 보안 네트워킹 프로토콜에서 사용
<div align="center">
<img src="https://github.com/user-attachments/assets/6ee01fc7-d4bc-44a5-9a2b-eab5b381f838">
</div>

3. 공개키 암호 방법이 유용하려면 자신이 통신하고자 하는 상대 개체(사람, 라우터, 브라우저 등)의 실제 공개키를 갖고 있는지 확인할 수 있어야 함
4. 공개키가 어떤 특정한 통신 개체의 것인지 보증하는 일은 일반적으로 인증 기관(Certification Authority, CA)에서 담당
   - 신원을 확인하고 인증서를 발행하는 것이 주 목적
   - 역할
     + CA는 어떤 개체(사람, 라우터 등) 스스로 주장하는 자신의 신분, 바로 그 개체가 맞는지 확인
       * 인증이 어떻게 수행되는지에 대한 정해진 과정은 없으며, CA와 관련해서는 CA가 적절한 방법으로 엄격하게 식별자 검증을 수행하리라는 점을 신뢰해야 함
     + 일단 CA가 개체의 신원을 확인하면, CA는 그 개체의 공개키와 신분확인서를 결합한 인증서를 만듬
       * 이 인증서는 공개키와 함께 공개키의 주인에 대해 고유한 식별 정보(예) 사람 이름 또는 IP 주소)를 담고 있으며, 인증서에는 CA가 전자 서명을 함
<div align="center">
<img src="https://github.com/user-attachments/assets/c6bd83fd-0c70-4ef8-98b4-d1b9db886edd">
</div>

   - 즉, CA가 서명한 인증서를 함께 보내며, CA의 공개키를 사용하여 인증서의 유효성을 검사하고, 공개키를 뽑아냄

5. 국제전기통신연합(International Telecommunication Union, ITU)과 IETE는 CA를 위한 표준 개발
   - ITU X.509는 인증서를 위한 상세 문법 뿐만 아니라 인증 서비스 제공
   - RFC 1422는 보안 인터넷 전자메일에 사용하기 위한 CA 기반 키 관리를 다룸 (X.509와 호환되지만 키 관리 구조를 위한 과정과 합의를 규정한다는 점에서 범위가 넓음)

6. 인증서의 주요 필드
<div align="center">
<img src="https://github.com/user-attachments/assets/04a85d10-ec44-4e33-a192-02203fef6166">
</div>
