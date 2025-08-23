-----
### 순환 중복 검사 (CRC)
-----
1. 컴퓨터 네트워크에서 널리 사용되는 오류 검출 기술
2. CRC 코드는 다항식 코드(Polynomial Code)로도 알려져 있음
   - 전송되는 비트열에 있는 0과 1 값을 계수로 갖는 다항식처럼 비트열을 생각할 수 있고, 또한 비트열에 적용되는 연산을 다항식 연산으로 이해하는 것이 가능하기 때문임

3. d비트로 이루어진 데이터 D를 송신 노드가 수신 노드로 전송한다고 가정
   - 먼저 송신자와 수신자는 G로 표기되는 생성자(Generator)로 알려진 r + 1 비트 패턴에 합의
   - G의 최상위(가장 왼쪽) 비트는 1이어야 함
<div align="center">
<img src="https://github.com/user-attachments/assets/6e0d0736-b304-4a15-87ca-2c0246b810c0">
</div>

   - 주어진 데이터 D에 대해 송신자는 r개의 추가 비트 R를 선택해서 D 뒤에 덧붙이며, 이 이진수로 해석되는 d + r 비트 패턴은 모듈로 2 연산을 이용하면 G로 정확히 나누어짐
   - 수신자는 d + r개의 수신 비트를 G로 나누며, 만일 나머지가 0이 아니면 오류가 발생한 것으로, 그렇지 않으면 데이터가 정확한 것으로 판정할 수 있음

4. 모든 CRC 검사는 덧셈의 올림(Carry)이나 뺄셈의 빌림(Borrow)이 없는 모듈로 2 연산을 사용
   - 덧셈과 밸셈이 동일함을 뜻하며, 모두 피연산자를 비트별로 XOR 한 것과 같음
<div align="center">
<img src="https://github.com/user-attachments/assets/21a0f432-30d1-43f8-9d8f-e4ae71995c16">
</div>

   - 일반 이진 연산에서처럼, $2^k$을 곱하는 것은 비트 패턴을 k개의 위치만큼 왼쪽으로 이동하는 것
   - 주어진 D와 R에 대해 $D · 2^{r} XOR R$은 d + r비트 패턴을 만들어 냄

5. 다음과 같은 식을 만족하는 n이 있도록 하는 R을 구해야 함
<div align="center">
<img src="https://github.com/user-attachments/assets/cc6dbef1-c391-49e4-92ba-b269b922feb4">
</div>

   - 즉, $D · 2^{r} XOR R$을 나머지 없이 G로 나눌 수 있도록 R을 선택해야 함
   - 이 식 양쪽에 R을 XOR(즉, 올림 없는 모듈로 2 덧셈)을 하면 다음과 같음
<div align="center">
<img src="https://github.com/user-attachments/assets/f337f811-cbe7-4109-bca7-ef1c346412ed">
</div>

   - 이 식은 $D · 2^{r}$을 G으로 나누면 나머지가 정확히 R이 되는 것을 뜻하므로, R 계산 가능
<div align="center">
<img src="https://github.com/user-attachments/assets/c6e3c816-6ab1-4155-a349-f0ab1218d5e7">
</div>

6. 예제
<div align="center">
<img src="https://github.com/user-attachments/assets/821f244d-1e2e-4e80-90b9-b223d4cdd10e">
</div>

   - D = 101110, d = 6, G = 1001, r = 3인 경우
   - 전송되는 9개의 비트는 101110011
   - $D · 2^{r} = 101011 · G XOR R$

7. 국제 표준으로는 8비트, 12비트, 16비트, 32비트 생성자 G가 정의
   - 다수의 링크 계층 IEEE 프로토콜에서 채택한 CRC-32 32비트 표준은 다음과 같은 생성자 사용
<div align="center">
<img src="https://github.com/user-attachments/assets/8dd4c010-284a-4f9d-bc87-a3ff45db49dc">
</div>

   - 각각의 CRC 표준은 r + 1 비트보다 적은 수 버스트 오류 검출 가능 (즉, r개 이하 연속적 비트 오류 모두 검출 가능)
   - 또한, 적절하게 추정해보면 r + 1 비트보다 큰 길이의 버스트 오류는 $1 - 0.5^{r}$의 확률로 검출
   - 또한, 각 CRC 표준은 임의의 홀수개 비트 오류 검출 가능
