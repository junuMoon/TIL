# Introduction to Vectors

## Linear Combinations

- "You can't add apples and oranges": This is the reason for vectors
- The pair of two seperate numbers `v1` and `v2` produces a two-dimensional vector `v`
- Vector `v`
    1. two numbers
    2. arrow from (0, 0)
    3. point in the plane
- Linear combination(`cv + dw`): Adding vectors and multiplying by scalars
- Pictur of combinations
    1. The combinations `cu` fill a *line* through zero vector
    2. The combinations `cu + dw` fill a *plane* through the vector
    3. The combinations `cu + dw + ew` fill three-dimensional *space* inclduing zero vector
- The vectors `cv` lie along a line. When `w` is not on that line, the combinations `cv + dw` fill the whole tow-dimensional plane
- The zero vector is always a possible combination = Every time we see a "space" of vectors, there will be zero vector

### Worked examples

1. `v = (1, 1, 0)` and `w = (0, 1, 1)`, Describe that plane and find a vector that is not a combinations of `v` and `w`
    - The plane of `(c, c+d, d)`
    - Dot product to perpendicular vector `(1, -1, 1)` results 0
2. For `v = (1, 0)` and `w = (0, 1)`, describe all points `cv` with `c >= 0` and all `cv + dw`
    - All points `cv` with whole c nonnegative numbers = X axis ge 0
    - `cv + dw` = first and fourth qudrant
3. Find two equations for c and d so that the linear combination `cv + dw = b`
    - `v = (2, -1), w = (-1, 2), b = (1, 0)`
    - `c = 2/3, d = 1/3`
    - `cv + dw = (2/3, 1/3)`
    - Final linear combination equation: `c1v1 + ... + cnvn = b`

### Notes

- All sums of diagonal vectors are linear combination of `cv + dw`
- Parallelogram: 평행사변형
- Problem 14: Moving the origin of 6:00 adds `j = (0, 1)` to every vector. So the sum of twelve vectors changes from `0 to 12j  = (0, 12)`


## Lengths and Dot Products

- The dot product of inner product(내적) of `v = (v1, v2)` and `w = (w1, w2)` is `v • w = v1w1 + v2w2`
- Dot product is zero means that the vectors are perpendicular, the angle between them is 90 degrees
- `v • v = length ** 2`
    - `||v|| = root(v • v)`
    - Pythagoras formula: `v1 ** 2 + v2 ** 2 = ||v|| ** 2`
- Unit vector: a vector whose length equals 1
    - `||u|| = 1`
    - In xy plane, unit vector is `(cos𝜃, sin𝜃)
- `u = v / ||v||` is a unit vector in the same direction as v
    - `v = (1, 1)`: `u = (1/√2, 1/√2)`
- Right angles produce `v dot w = 0`
    - The zero vector `v = 0` is perpendicular to every vector `w` because `0 dot w = 0`
- The angle is less then `1/2 pie` when `v dot w` is positive
- The angle is more thant `1/2 pie` when `v dot w` is negative
- Unit vectors `u` and `U` at angle `𝜃` produce `u dot U = cos 𝜃`
- `v dot w / ||v|| ||w|| = cos 𝜃`
    - `u = v / ||v||`
    - `U = w / ||w||`
- Schewarz inequality: `|v dot w| <= ||v|| ||w||`
- Traingle inequuality: `||v + w|| <= ||v|| + ||w||`
    - (length of `v + w`) <= (length of `v`) + (length of `w`)

```python
v = np.array([1, 2])
w = np.array([2, 1])
v @ w # 4
norm_v = norm_w = (v @ v) ** 0.5 # sqrt(5)
cos = (w @ v) / (norm_v * norm_w) # 0.7999999999999998
```
### Worked examples

- `v = (3, 4) and w = (4, 3)`
    - Schwarz inequality: `24 <= 25`
    - Triangle inequality: `7 * sqrt(2) <= 5 + 5`
    - Cosine of angle between `v` and `w`: `24 / 25`
- `v = (3, 4)`
    - Unit vector `u = (3/5, 4/5)`
    - Perpendicular unit vector `U = (4/5, -3/5) and -(4/5, 3/5)`
- `r = (2, -1), s = (-1, 2)`, `x dot r = 1 and x dot s = 0`
    - vector x perpendicular to s: `(2d, d)`
    - vector x perpendicular to s and dot product has 1 with r: `(2/3, 1/3)`

> Section 1.1 would start with columns `vj`. The goal is to product `x1v1 + ... + xnvn = b`. This section would start from rows `ri`. The goal is to find `x dot ri = bi`. Soon the `v`s will be the columns of a matrix A, and the `r`s will be the rows of A. Then the (one and only) problem will be to solve `Ax = b`.

### Notes

- 산술평균(Arithmetic Mean): `(x1 + ... + xn) / n`
    - 극단치가 없는 경우에는 대표값으로 사용하기에 적당
- 기하평균(Geomtric Mean): `(x1 * ... * xn) ** (1/n)`
    - 구간별 변화율 데이터로부터 전체 구간에 대한 평균 변화율
- 조화평균(Harmonic Mean): `n / (1/x1 + ... + 1/xn)`
    - 구간별 평균속력 데이터로부터 전체 구간에 대한 평균 속력
- Hypotenuse: 빗변

## Matrices

- `Ax=b`
    - combinations of columns of A
    - dot products of rows of A and vector x
- Question:
    - Old: Compute the linear combination `x1u + x2v + x3w` to find `b`
    - New: Which combination of `u, v, w` produces a particular vector `b`
- The key question is whether the third vector is in that plane
    - Whether vector `w` is a linear combination of `u` and `v`
- Independent columns: `w` is not in the plane of `u and v`
    - No combination except `0u+0v+0w = 0` gives `b = 0`
    - `Ax = 0` has one solution
    - `A` is invertible matrix
- Dependent columns: `w` is in the plane of `u and v`
    - `u + v + w` give `b = 0`
    - `Cx = 0` has many solutions or none
    - `A` is not singular matrix
    - Singular matrix: 특이행렬(역행렬이 존재하지 않음)
- Triangular matrix: 삼각행렬은 정사각행렬의 특수한 경우로, 주대각선을 기준으로 대각항의 위쪽이나 아래쪽 항들의 값이 모두 0인 경

### Worked examples

- The three columns of A are still independent. They don't lie in a plane. The combinations of those three columns, using the right weights `x1, x2, x3` can product any three-dimensional vector `b = (b1, b2, b3)`. Thos weights come from `x = I(A)b`
- 