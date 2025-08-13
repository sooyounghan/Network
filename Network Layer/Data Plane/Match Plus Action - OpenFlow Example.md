-----
### 매치 플러스 액션 작업의 OpenFlow 예
-----
1. 네트워크에는 6개의 호스트(h1, h2, h3, h4, h5, h6)와 3개의 패킷 스위치(s1, s2, s3)가 존재하며 각 4개의 로컬 인터페이스(1, 2, 3, 4)가 존재
2. 이 동작을 구현하는데 필요한 s1, s2, s3의 플로우 테이블 엔트리를 고려
3. 첫번째 예 : 간단한 포워딩
   - 포워딩 동작이 h5 또는 h6에서 h3 또는 h4의 패킷이 s3에서 s1로 전달된 다음, s1에서 s2로 전달된다고 가정 (s3과 s2 사이 링크 사용 완전 차단 가능)
<div align="center">
<img src="https://github.com/user-attachments/assets/d778d58c-606e-40aa-95d1-6eb65f83db02">
</div>

   - s1의 플로우 테이블 엔트리
<div align="center">
<img src="https://github.com/user-attachments/assets/5b6bb7b2-ad53-4776-839c-e68e00d8fd8d">
</div>

   - s3에 플로우 테이블 엔트리가 필요하므로 h5 또는 h6에서 전송된 데이터그램은 인터페이스 3을 통해 s1로 전달
<div align="center">
<img src="https://github.com/user-attachments/assets/abae1fa8-b179-4d54-a380-e5bcc9a33883">
</div>

   - 마지막으로 s1에 도착한 데이터그램을 호스트 h3 또는 h4로 전달할 수 있도록 s2의 플로우 테이블 엔트리 필요
<div align="center">
<img src="https://github.com/user-attachments/assets/3151d541-2ea4-48e4-8e09-7f8b4850d8c3">
</div>

4. 두번쨰 예 : 로드 밸런싱
   - h3에서 ```10.1.*.*```로 향하는 데이터그램이 s2과 s1 사이의 링크로 전달되는 반면, h4에서 ```10.1.*.*```로의 데이터그램은 s2과 s3 사이 링크로 전달되는 로드 밸런싱 시나리오 고려 : 이 동작은 IP의 목적지 기반 포워딩으로 수행될 수 없으므로, s2의 플로우 테이블은 다음과 같음
<div align="center">
<img src="https://github.com/user-attachments/assets/98c05af0-be57-4375-be5a-5344a733d5f9">
</div>

   - s2에서 수신한 데이터그램을 h1 또는 h2로 전달하려면 s1에서 플로우 테이블 엔트리가 필요
   - 인터페이스 4에서 수신한 데이터그램을 s2에서 인터페이스 3을 통해 s1로 전달하려면 s3에서 플로우 테이블 엔트리가 필요

5. 세 번째 예 : 방화벽
   - s2가 s3에 연결된 호스트에서 보낸 트래픽만 수신하도록 방화벽 시나리오
<div align="center">
<img src="https://github.com/user-attachments/assets/3b840985-bfcb-40a0-a985-adc1dfb1bd82">
</div>

   - s2 플로우 테이블에 다른 엔트리가 없으면 다른 엔트리가 없으면 ```10.3.*.*```의 트래픽만 s2로 연결된 호스트로 전달

6. 매치 플러스 액션 테이블은 사실 제한된 형태의 프로그래밍 기능성이며, 데이터그램 헤더값과 매치 조건 사이 매치를 기반으로 라우터가 데이터그램을 전달하고 조작하는 방법 명시
