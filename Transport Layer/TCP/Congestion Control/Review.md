-----
### TCP 혼잡 제어 : 복습
-----
1. 연결이 시작되고 초기 슬로 스타트 기간을 무시하고, 손실이 타임아웃이 아니라 3개의 중복 ACK로 표시된다고 가정
2. TCP 혼잡 제어는 RTT마다 1 MSS씩 cwnd의 선형(가법적인) 증가와 3개의 중복 ACK 이벤트에서 cwnd의 절반화(승법적 감소)
3. 이러한 이유로 TCP 혼잡 제어는 가법적 증가, 승법적 가소(Additive-Increase, Multiplicative Decrease, AIMD)의 혼잡 제어 방식이라고 함
<div align="center">
<img src="https://github.com/user-attachments/assets/82577389-c7b3-4d98-9ac9-a7e905d9ae05">
</div>

  - 톱니 동작이 생기게 하는데, 대역폭에 대한 TCP 탐색의 초기 직관을 보여줌
  - TCP는 3개의 중복 ACK가 발생할 때까지 선형으로 그 혼잡 윈도 크기를 (결국 전송률) 증가시킴
  - 그리고 나서 혼잡 윈도 크기를 반으로 감소시키지만, 다시 추가적인 가용 대역폭이 있는지 탐색하기 위해 선형으로 증가시키기 시작
