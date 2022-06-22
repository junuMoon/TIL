# Mel Spectrum
1. 스펙트럼(Spectrum): 입력 음성을 짧은 구간으로 나눈 Frame들에 각각 푸리에 변환 -> 주파수 정보를 추출
2. 멜스펙트럼(Mel Spectrum): 말소리 인식에 민감한 주파수 영역대를 주요하게 보는 Mel Filter Bank를 적용

## Raw Wave Signal
`sample_rate, signal = spicy.io.wavefile.read(‘example.wav’)`

- `sample_rate`: 1초에 몇 번 음성 신호를 샘플하는지
	- 16000(16khz): 실수 범위의 이산 음성 신호가 -32768(2^15)~32767(2^15-1) 범위의 정수로 변환되었다는 뜻
- `signal`:  변환된 시퀀스
	- `signal`의 length를 `sample_rate`로 나누면 입력 음성의 총 길이를 알 수 있음
	- `len(signal) / sample_rate = 11.455`

## Framing & Windowing
- Framing: 음성 신호가 stationary하다고 가정해도 좋을 만큼 원시 음성 신호를 아주 짧은 시간 단위(대개 25ms)로 잘게 쪼개기
	- `frame_size`: frame 시간 단위
	- `frame_stride`: frame 간에 겹치는 시간
	- `frame_length = frame_size * sample_rate`: 1frame의 데이터 사이즈
	- `frame_step = frame_stride * sample_rate`
- Windowing:각각의 프레임에 특정 함수를 적용해 경계를 스무딩하는 기법
	- 입력 신호를 인위적으로 자르는 Framing의 경우 자른 부분에서 직각 신호(square wave)가 발생하는 것을 해결
	- 직각 신호는 사인함수를 엄청 많이 더해야나오는 엄청난 고주파

## Magnitude & Power
-  푸리에 변환의 결과는 복소수로 실수부(x축)와 허수부(y축)로 이뤄짐
	- `X[k] = a + b * j`
- Magnitude(진폭): 주파수 성분의 크기
	- `√(a^2 + b^2)`
- Phase(위상): 주파수의 복소평면상 단위원에서의 위치
	- `arctan(b/a) = 𝜃, where tan𝜃 = a/b` 
	- `arctan`: 탄젠트(tan x)를 분모로 내린 역함수(x=tan y)
- MFCC를 위해 음성 인식이 불필요한 위상 정보는 없애고 진폭 정보만을 남김
	- `abs(3.53+4j) = 5.334`
- Power = `abs(X[k]) ^ 2 / N`

## Filter Banks
![mel scale filter](https://i.imgur.com/vuMPDsy.jpg)

- 필터뱅크: 특정 주파수에 가중치를 주는 방법
	- 사실상 Linear Combination
- 멜스케일필터: 저주파수 영역대를 세밀하게/고주파수 영역대를 넓게 살피는 필터
	- 사람은 저주파수를 더 잘 인식하는 것에서 따옴
- Log-Mel Spectrum: 사람의 소리 인식은 log 스케일을 따르기 때문에 spectrum에 log를 취해줌






