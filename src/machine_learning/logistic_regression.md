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
- logistic function(sigmoid): `1 / (1 + e^-๐)`
    - ๐ = `w.T@x + b`
    - range: [0, 1]

```python
prob = 0.8
odds = prob / (1-prob)  # 4.0
log_odds = np.log(odds)  # 1.38
prob = 1 / (1 + np.exp(-log_odds))  # 0.8
```

## Maximum Likelihood Estimation

- How to fit logistic regression model to data
- Logit range from -inf to inf so that we can't use least-squares to find best fitting line
- Values of logistic function range from 0 to 1 so we can use least-squares to find best fitting line
- Instead, we use maximum likelihood to find best fitting line
    - Likelihood function: `P(x|๐)` = `P(x1, x2, x3, ..., xn | ๐)`
         - `(0.9 * 0.8 * ... * (1-0.2) * (1-0.1))`
    - Log-likelihood function: `L(๐|x)` = `Sum 1 to n log(P(xi|๐))`
        - `log(0.9) + log(0.8) + ... + log(1-0.2) + log(1-0.1)`
- To maximizie likelihood equals to minimize negative log-likelihood

> ๋ฐ์ดํฐ๊ฐ ์์์ ํ๋ผ๋ฉํฐ ฮธ์ ์์กดํ๋ ํ๋ฅ ๋ถํฌ๋ฅผ ๋ฐ๋ฆ. `P(v1, ..., vn | ฮธ)`๋ฅผ ๊ตฌํ๊ณ  ์ถ์๋ฐ ฮธ๋ฅผ ๋ชจ๋ฆ. ๋ฐ๋ผ์ ๋ฒ ์ด์ฆ ๊ท์น์ ํ์ฉํ์ฌ ฮธ๊ฐ ๋ฐ์ํ  ์ฐ๋(likelihood)๋ก ๋ฐ๊ฟ. `L(ฮธ|v1, ..., vn)`๋ฅผ ์ต๋ํํ๋ ฮธ๋ฅผ ์ฐพ๋๋ค. ๊ด์ธก๋ ๋ฐ์ดํฐ๊ฐ ๋ฐ์ํ  ๊ฒฝ์ฐ๋ฅผ ๊ฐ์ฅ ๋๊ฒ ๋ง๋ค์ด์ฃผ๋ ๊ฐ

### Notes

- z-value: tell you how many standard deviations the estimated coefficients are away from 0 on a standard normal distribution
- The z value for the intercept, -1.9, tells us that the estimated value for the intercept, -1.5 is less than 2 standard deviations from 0, and thus, not significantly different from 0