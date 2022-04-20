# Logistic Regression

- Depedent variable in logistic regression is the probability of the class which is 0 or 1
- Linear regression(`wx + b`) isn't appropriate for this problem because its range is [-inf, inf]
- So we convert probability to logit which range is [-inf, inf]
- And put it into sigmoid function which range is [0, 1] 
- Logistic regression is the exact same as good old linear models except the coefficients are in terms of th logit: log(odds)

![logit-sigmoid](https://user-images.githubusercontent.com/31475037/60703569-17a4ab80-9f3d-11e9-8b3b-10507d77d199.PNG)


## Odds and Log(Odds)

- p: probability of class
    - range: [0, 1]
- odds = `p / 1-p`
    - range: [0, inf]
- logit = log(odds) = log(p) - log(1-p) = log(p / 1-p)
    - range: [-inf, inf]
- logistic function(sigmoid): `1 / (1 + e^-𝜃)`
    - 𝜃 = `w^Tx + b`
    - range: [0, 1]

## Maximum Likelihood

- How to fit logistic regression model to data
- Logit range from -inf to inf so that we can't use least-squares to find best fitting line
- Values of logistic function range from 0 to 1 so we can use least-squares to find best fitting line
- Instead, we use maximum likelihood to find best fitting line
    - maximize likelihood = `(0.9 + 0.8 + ... + (1-0.2) + (1-0.1))`
    - maximize log-likelihood = `log(0.9) + log(0.8) + ... + log(1-0.2) + log(1-0.1)`
    - equals to minimize negative log-likelihood

> 데이터가 임의의 파라메터 θ에 의존하는 확률분포를 따름. `P(v1, ..., vn | θ)`를 구하고 싶은데 θ를 모름. 따라서 베이즈 규칙을 활용하여 θ가 발생할 우도(likelihood)로 바꿈. `L(θ|v1, ..., vn)`를 최대화하는 θ를 찾는다. 관측된 데이터가 발생할 경우를 가장 높게 만들어주는 값

### Notes

- z-value: tell you how many standard deviations the estimated coefficients are away from 0 on a standard normal distribution
- The z value for the intercept, -1.9, tells us that the estimated value for the intercept, -1.5 is less than 2 standard deviations from 0, and thus, not significantly different from 0