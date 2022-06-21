# Automatic Speech Recognition in Bayesian

`Y-hat = argmaxP(X|Y)P(Y)`

- 음향모델: P(X|Y)
	- 음소/단어 시퀀스(Y)가 주어졌을 때 음성 신호(X)가 나타날 확률
	- 음성 신호와 음소/단어의 관계를 표현
- 언어모델: P(Y)
	- 음소/단어 시퀀스의 확률분포
	- 시퀀스 Y가 얼마나 그럴듯한지(likely)

## Bayesian Learning

`P(h|D) = P(D|h)P(h) / P(D)`

- 패턴(데이터: 음성)를 보고 패턴의 원인(가설: 음소/단어)을 역추정
- P(h|D): 사후 확률(posterior probability)
- P(h): 사전 확률(prior probability)
- P(D|h): 가능도(likelihood)
- P(D): 경계 확률
	- 상수로 취급

### Maximum Likelihood Estimation

`dE(𝜃) := 0`

- 가능도를 최대로하는 paratmeter 𝜃를 찾는 과정
- 가능도(Likelihood): 데이터 X가 𝜃=(μ, 𝜎)를 갖는 분포로부터 만들어졌을(generated) 확률
	- `P(D|𝜃) = P(D1|𝜃) * P(D2|𝜃) * … * P(Dn|𝜃)`
- `-log`를 취한 log likelihood값을 미분하여 0이되는 값(극솟값)을 찾는다
	- `E(𝜃) = -lnP(D|𝜃) = -lnP(D1|𝜃) + -lnP(D2|𝜃) + … + -lnP(Dn|𝜃)`

### Maximum A Posterior Estimation

`argmaxP(𝜃|D) = argmaxP(D|𝜃)P(𝜃)`

- 사후확률을 최대로하는 paratmeter 𝜃를 찾는 과정
- 사후확률(Posterior): 데이터 X가 𝜃에 속할 확률
	- P(D|𝜃) * P(𝜃) = Likelihood * prior
- `Likelihood * prior`를 최대로 만드는 𝜃를 찾는 것

