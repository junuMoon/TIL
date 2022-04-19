# Solving Linear Equations

## Vectors and Linear Equations

- When `b = 0`, a combination of columns of `Ax` is zero: one possibility is `x = (0, ... , 0)`
- When `b = 0`, all the palnes `(row i) dot x = 0` go through the center point `x = (0, ... , 0)`
- Linear means that the unknowns are only muplied by numbers
- If you separate the original system into its columns instead of its rows, you get a vector equation
    - The row picture shows three planes meeting at a single point
    - The column picture combines three columns to product vector b
- Coefficient matrix: 계수행렬, matrix A in `Ax = b`
- Identity matrix: 단위행렬, `Ix = x`
- Permutation matrix: 치환행렬, 'I dot (x, y) = (y, x)'

### Worked examples

1. To show that `(0, -1, 0)` is the only solution we have to know that "A is invertible" and "the columns are independent" and "the determinant is not zero"