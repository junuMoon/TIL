# Discrete Fourier Transform

`Xk = ´∑xn * exp(n * -2iπ * k/N)`

시간에 대한 함수(혹은 신호)와 주파수에 대한 함수를 잇는 수학적인 연산

## 복소 지수 함수 CIS

`cis(𝜃) = exp(i𝜃) = cos𝜃 + i*sin𝜃𝜃`

- Euler’s Formula:  `exp(iπ) + 1 = 0`
- `exp(I𝜃)`는 복소 평면상 반지름이 1인 단위원
	- 복소부와 실수부로 구성
	- x축 실수부
	- y축 허수부
- 복소지수함수를 푸리에 변환 수식에 적용하면
	- `𝜃 = n * -2iπ * k/N`
	- `Xk = ∑xn * [cos(n * 2iπ * k/N) - i * sin(n * 2iπ * k/N)]`
- `xn`: 시간 도메인의 n번째 샘플
- `Xk`: 주파수 도메인의 k번째 푸리에 변환 결과물 -> 주파수 성분
- `k/N`: 복소평면상 단위원에서 얼마나 빠른 속도로 회전하는지

## DFT matrix

`X = Wx`

[image:70306276-9696-4AD6-BC68-B7D6F9BA7A16-11551-00001667600F278B/6680B19E-7052-426C-BABA-C75084F0F2B9.png]
- W의 각 행은 복소평면상 단위원에서 도는 각기 다른 각 속도
- 이산 푸리에 변환의 본질은 선형 변환(linear transform)
- `x`: input signal
- `W = (w^kn / √N)`
	- N X N matrix 
	- 행 인덱스는 k, 열 인덱스는 n
	- Note that the normalization factor in front of the sum(`1/√N`)
- `w = exp(-2πi/N)`
- `W[k, n] = w^kn = exp(-2πi/N * k * n) `

