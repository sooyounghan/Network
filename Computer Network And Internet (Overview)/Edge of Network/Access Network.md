-----
### 호스트와 종단 시스템
-----
<div align="center">
<img src="https://github.com/user-attachments/assets/3d922572-e031-48c3-82a6-2e8c99656de5">
</div>

1. 종단 시스템은 웹 브라우저 프로그램, 웹 서버 프로그램과 같은 애플리케이션을 수행하므로 호스트(Host)라고 부름
2. 따라서, 호스트와 종단 시스템을 혼용
3. 호스트는 때떄로, 클라이언트(Client)와 서버(Server)로 구분되며, 비공식적으로 클라이언트는 데스크톱, 이동 PC, 스마트폰 등 의미

-----
### 접속 네트워크 (Access Network)
-----
<div align="center">
<img src="https://github.com/user-attachments/assets/0bff40ea-d1b9-47f4-a747-1fe1940c5ab9">
</div>

1. 가장자리 라우터(Edge Router) : 종단 시스템을 그 종단 시스템으로부터 먼 거리에 있는 다른 종단 시스템까지의 경로상에 있는 네트워크
2. DSL (Digital Subscriber Line)과 케이블 : 오늘날 가장 널리 보급된 광대역 가정 접속 유형
<div align="center">
<img src="https://github.com/user-attachments/assets/419f4c41-d90d-46fd-b6dd-4d96e6ca83a1">
</div>

   - DSL를 사용할 때는 고객의 텔코(Telco)가 ISP가 되기도 하며, 각 고객의 DSL 모뎀은 텔코의 중앙 지역국(Central Office, CO)에 위치한 DSLAM(Digital Subscriber Line Access Multiplexer)과 데이터를 교환하기 위해 기존 전화 회선을 사용함
   - 가정의 DSL 모뎀은 디지털 데이터를 받아 전화선을 통해 CO로 전송하기 위해 고주파 신호로 변환
   - 여러 가정으로부터의 아날로그 신호는 DSLAM에서 디지털 포맷으로 다시 변환
   - 이 방식은 DSL 링크가 3개의 분리된 링크인 것처럼 보이게 하여, 하나의 전화 회선과 인터넷 연결이 동시에 DSL 링크를 공유할 수 있도록 함(= 주파수 분할 다중화)
     + 고속 다운스트림 채널 (50 kHz ~ 1 MHz 대역)
     + 중간 속도 업 스트림 채널 (4 ~ 50kHz 대역)
     + 일반적인 양방향 전화 채널 (0 ~ 4kHz 대역)

   - 고객 쪽의 스플리터(Spliter)는 가정에 도착하는 데이터와 전화 신호를 분리하고, 데이터 신호를 DSL 모뎀에 전송
   - 텔코 쪽에 있는 CO의 DSLAM은 데이터와 전화 신호를 분리하고, 데이터를 인터넷으로 송신 (수백 혹은 수천 개의 가정들이 하나의 DSLAM에 연결)
   - DSL 표준은 24 Mbps와 52 Mbps 속도의 다운 스트림과 3.5 Mbps와 16 Mbps 속도의 업스트림을 포함하는 여러 전송률을 정의 (최신 표준은 이 둘을 결합한 1Gbps 속도로 정의) : 둘의 속도가 다르므로 이 접속 방식을 비대칭(Asymmetric)

3. HFC (Hybrid Fiber Coax) : 광 케이블과 동축 케이블을 사용하는 방식
<div align="center">
<img src="https://github.com/user-attachments/assets/166bfc63-192e-483b-9707-a33fdee2574e">
</div>

   - 케이블 인터넷 접속 방식 (Cable Internet Access) : 가정은 케이블 TV 서비스를 제공하는 같은 회사로부터 인터넷 접속 서비스를 받음
   - 광 케이블은 케이블 헤드엔드(Head End)를 이웃 레벨 정션(Junction)에 연결하며, 이로부터 개별 가정에 도달하는 전통적인 동축 케이블을 사용
   - 케이블 모뎀이라고 하는 특별한 모뎀이 필요한데, 외장형 장치이며, 이더넷 포트를 통해 가정 PC에 연결
   - CMTS(Cable Modem Termination System) : DSL에서 DSLAM과 유사한 기능 (많은 다운 스트림 가정에 있는 케이블 모뎀으로부터 송신된 아날로그 신호를 다시 디지털 포맷으로 변환)
   - 케이블 모뎀은 HFC 네트워크를 2개의 채널(업 스트림과 다운 스트림)로 나누며, 접속은 비대칭, 다운 스트림이 업 스트림 채널보다 빠른 전송률 할당
   - 공유 방송 매체로서, 헤드엔드가 보낸 모든 패킷이 모든 링크의 다운 스트림 채널을 통해 모든 가정으로 전달되며, 가정에서 보낸 모든 패킷은 업스트림 채널을 통해 헤드엔드로 전달

4. FTTH(Fiber To The Home) : CO로부터 가정까지 직접 광섬유 경로를 제공
   - 가장 간단한 광신호 분배 네트워크 : 다이렉트 광섬유(Direct Fiber) - 각 가정으로 CO에서 하나의 광섬유를 제공
   - 일반적으로 사용되는 것은 가정에 가장 가까운 하나의 광섬유로 와서 고객별 광섬유로 분리되는데, 이러한 스플리팅(Splitting)을 수행하는 두 가지 경쟁적인 광신호 분배 네트워크 구조 : AON(Active Optical Network), PON(Passive Optical Network)
     + AON은 근본적으로 교환 이더넷

<div align="center">
<img src="https://github.com/user-attachments/assets/52b615a2-dc9a-4874-afa2-d32f7564adef">
</div>

   - PON 분배 구조를 이용하는 FTTH로서, 각 가정은 ONT(Optical Network Terminator)를 가지고 있으며, 지정된 광섬유로 이웃 스플리터에 연결
   - 스플리터는 여러 가정을 하나의 공유 광섬유로 결합하고, 이를 텔코의 CO에 있는 OLT(Optical Line Terminator)에 연결
   - 광신호와 전기신호 간의 변환을 제공하는 OLT는 텔코 라우터를 통해 인터넷에 연결
   - 가정에서는 홈 라우터(무선 라우터)를 ONT에 연결하고 홈 라우터를 통해 인터넷에 접속
   - PON 구조의 OLT에서 스플리터로 송신된 모든 패킷은 스플리터(케이블 헤드엔드와 유사)에서 복제

5. 5G 고정 무선 (5G Fixed Wireless, 5G-FW)
   - 빔 포밍(Beam-Forming) 기술 사용
   - 서비스 제공자의 기지국에서 가정 내 모뎀으로 데이터를 무선으로 전송

6. LAN (Local Area Network) : 일반적으로 종단 시스템을 가장자리 라우터에 연결하는 데 사용
   - 이더넷은 이더넷 스위치에 연결하기 위해 꼬임 상선 사용
   - 무선 랜 환경에서 무선 사용자들은 기업 네트워크(대부분 유선 이더넷 포함)에 연결된 AP(Access Point)로 패킷을 송신 / 수신하고, 이 AP는 유선 네트워크에 다시 연결
   - 무선 랜(Wireless LAN) 사용자들은 일반적으로 AP 수십 미터 반경 내 있어야 함
<div align="center">
<img src="https://github.com/user-attachments/assets/780f27b1-c385-4375-a8d8-cc97017c6e90">
</div>
