-----
### RSA
-----
1. RSA 알고리즘(Ron Rivest, Adi Shamir, Leonard Adleman의 이름에서 유래)이 공개키 암호화와 거의 동의어처럼 취급됨
2. RSA는 모듈로 n 연산을 많이 사용
   - 모듈러 연산 : x mod n은 x를 n으로 나눈 나머지를 의미 (예) 19 mod 5 = 4이며, 모듈러 연산에서는 일반적인 덧셈, 곱셈, 지수승 등이 수행되지만, 각 연산의 결과가 그 결과값을 n으로 나눈 나머지로 대체)
   - 모듈러 연산의 유용한 성질
<div align="center">
<img src="https://github.com/user-attachments/assets/1ff5b765-8bcc-4df5-82ca-62c5d28c76ea">
</div>

   - 세 번째 성질로 부터 항등식 $(a \bmod n)^{d} \bmod n = a^{d} \bmod n$을 얻을 수 있음
   - 여기서는 메세지는 단지 비트열이고, 모든 비트열은 하나의 고유한 정수(비트열 길이도 함께) 나타난다고 가정 (예를 들면, 어떤 메세지가 비트열 1001인 경우 이 메세지는 십진수 9로 나타낼 수 있음)
   - 그러므로 RSA로 어떤 메세지를 암호화하는 것은 그 메세지를 나타내는 고유한 정수를 암호화하는 것

3. RSA와 관련된 두 가지 요소
   - 공개키와 개인키 선택
   - 암호화 / 복호화 알고리즘

4. 공개키와 개인키를 생성하기 위한 단계
   - 2개의 큰 소수 (Prime Number) p와 q를 선택 (값이 커질수록 RSA를 깨기가 어렵지만, 암호화와 복호화를 수행하는데도 많은 시간이 걸리는데, RSA 연구소에서는 p와 q의 곱이 1024비트 수준이 되어야 한다고 권장)
   - n = pq, z = (p - 1)(q - 1) 식을 계산
   - 1을 제외하고 z와 공통 인수가 없는 n보다 작은 수 e를 선택 (e와 z는 서로소 관계) : 이 값이 암호화 과정에서 사용되므로 문자 e 사용
   - ed - 1이 z로 정확히 나누어 떨어지는(나머지가 없는) 숫자 d를 찾음 : 복호화 과정에서 사용되므로 문자 d를 사용 (즉, e가 주어졌을 때 다음 식이 성립하도록 d를 선택)
<div align="center">
<img src="https://github.com/user-attachments/assets/81e93365-dbf9-4ada-a71b-be0ef19db2b4">
</div>

   - 모든 이가 사용할 수 있도록 공개한 밥의 공개키 $K^{+}_{B}$는 숫자 쌍 (n, e)
   - 개인키는 숫자 쌍 (n, d)

5. 암호화와 복호화 과정
   - 앨리스가 밥에게 정수 m(m < n)으로 표현되는 비트 패턴을 보낸다고 가정
   - 암호화를 위해 앨리스는 지수승 $m^{e}$를 수행하고, 이를 n으로 나누었을 때 나머지를 계산
   - 앨리스가 보내는 평문 메세지 m의 암호 값 c는 다음과 같음
<div align="center">
<img src="https://github.com/user-attachments/assets/1770412d-9eb9-452f-9d1c-347d388e4bbf">
</div>

   - 이 암호 값 c에 해당하는 비트 패턴이 밥에게 전송
   - 수신된 암호 메세지 c를 복호화하기 위해 밥은 다음 식을 수행 (개인키 (n, d) 필요)
<div align="center">
<img src="https://github.com/user-attachments/assets/25f39f6b-1206-4b2c-becd-74d091886827">
</div>

6. 예시
   - p = 5, q = 7을 선택한다고 가정
   - n = 35, z = 24가 되며, 5와 24가 공통 인수가 없으므로 e = 5를 선택
   - 5 * 29 - 1(ed -1)이 정확히 24로 나누어 떨어지므로, d = 29를 선택
   - n = 35, e = 5 두 값은 공개하고, d = 29를 비밀로 유지
   - 두 공개 값이 알려진 후 문자 'l', 'o', 'v', 'e'를 전송
   - 각 문자를 1과 26 사이 숫자로 바꾼 다음 암호화와 복호화 수행 (여기서는 4개 문자 각각 별개 메세지로 간주했으며, 실제적인 예에서는 4개의 문자가 각 8비트의 ASCII 코드로 변환되고 최종적으로 전체 32비트 패턴에 해당하는 정숫값이 암호화될 것)

<div align="center">
<img src="https://github.com/user-attachments/assets/c0ac4e2b-1cc9-49e2-8b24-fca4384081b1">
</div>

<div align="center">
<img src="https://github.com/user-attachments/assets/b34fcaa1-9d82-491a-b0c3-9ad3f9195a76">
</div>

   - 매우 간단함에도 불구하고, 매우 큰 수들이 나타남

-----
### 세션 키
-----
1. RSA에 필요한 지수 연산은 시간이 많이 필요한 작업으로, 실제로 RSA는 종종 대칭키 암호와 함께 사용
2. 예를 들어, 앨리스가 밥에게 대량의 암호화 데이터를 보내고자 할 때, 먼저 앨리스는 데이터 암호화에 사용할 키를 고르는데 이를 세션 키(Session Key)라고 하며 $K_{S}$로 표기
   - 세션키는 대칭키 암호화(예) DES나 AES)에 사용될 공유 비밀키 이므로 앨리스는 밥에게 이를 알려줘야 함
   - 앨리스는 밥의 공개키로 세션키를 암호화함
   - 즉, c = $(K_{S})^{e}$ mod n으로 계산
   - 밥은 세션키 RSA로 암호화된 형태인 c를 받고, 이를 복호화해서 세션키 $K_{S}$를 얻음
   - 따라서, 밥은 이제 앨리스가 데이터 암호화에 사용한 세션키를 사용

-----
### RSA의 동작
-----
1. n = pq이며, p와 q는 RSA 알고리즘에서 사용되는 큰 소수
2. RSA 암호화에서 메세지(고유한 하나의 정수로 표현되는) m은 모듈로 n 연산을 사용해 e 제곱을 함
<div align="center">
<img src="https://github.com/user-attachments/assets/981c4799-9244-454b-9df1-821b7817743d">
</div>

3. 복호화는 이 값에 다시 모듈로 n을 사용해 d 제곱을 하는데, 따라서 암호화 단계와 복호화 단계를 거친 값은 $(m^{e} \bmod n)^{d} \bmod n$
   - $(a \bmod n)^{d} \bmod n = a^{d} \bmod n$이 성립하므로, 다음과 같이 정리 가능
   - $a = m^{e}$이면,
<div align="center">
<img src="https://github.com/user-attachments/assets/2543ecfe-a2da-41a2-b2d0-e263fe8e7ddb">
</div>

   - $m^{ed} \bmod n = m$은 다음과 같이 정의 가능
     + p와 q가 소수이고, n = pq, z = (p - 1)(q - 1)이면, $x^{y} \bmod n = x^{y \bmod z} \bmod n$과 같다는 성질이 필요
     + x = m이고, y = ed이면,
<div align="center">
<img src="https://github.com/user-attachments/assets/20e94cc2-7f59-44a9-8029-c2c1e8168300">
</div>

  - 여기서 ed mod z = 1이 되도록 e와 d를 선택했으므로,
<div align="center">
<img src="https://github.com/user-attachments/assets/62a89595-030b-495e-84a3-a0ef7b7b8018">
</div>

   - 먼저 e 제곱(암호회)를 한 다음, d 제곱(복호화)를 하면 원래 값 m을 얻게 되며, d 제곱을 하고, e 제곱을 하더라도, 즉 암호화와 복호화 순서를 바꿔서 하더라도 원래의 값 m을 얻을 수 있음
<div align="center">
<img src="https://github.com/user-attachments/assets/6e773f8f-898f-46da-a8c7-faa01f3661a8">
</div>

4. RSA 보안은 공개 값 n을 인수분해하여 p와 q를 찾는 빠른 알고리즘이 알려져 있지 않다는 점에 기반
   - 만일 소수 p와 q, 그리고 주어진 공개 값 e를 알고 있다면 비밀키 d를 쉽게 찾을 수 있음
   - 하지만, 숫자를 인수분해하는 빠른 알고리즘이 존재하는지 아닌지 확실히 알 수 없으므로, RSA 보안도 완벽히 보장된다고 할 수 없음

5. 디피-헬만 알고리즘은 널리 사용되는 공개키 암호화 알고리즘
   - 다만, 임의의 길이 메세지를 암호화할 수 없다는 점에서 RSA만큼 유용하지 않음
   - 하지만 메세지를 암호화하기 위해 대칭 세션키를 생성하는데 사용 가능
