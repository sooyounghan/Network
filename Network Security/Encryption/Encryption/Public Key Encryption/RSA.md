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
