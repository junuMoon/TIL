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

## The Idea of Elimination

- Elimination produces an upper triangular matrix(U)
- To elminate x: Subtract a multiple of equation 1 from equation 2
    - Pivot: first nonzero in the row that does the elmination
    - Multiplier: (Entry to eliminate) divided by (pivot)
- Gaussian Elimination: `Ax = b` -> `Ux = c`
    - It is non-singular if there is a full set of n pivots(never zero!)

## Elimination Using matrices

- `E`: Elimination matrix
- The purpose of E31 is to produce a zero in the (3, 1) position of the matrix
- Entry: component for a vector
    - `aij = A(i, j)`
- The solution `x` is not changed by elimination. It is the coefficient matrix that is changed
    - `EAx = Eb`
- Augemented matrix: `[A b]`
    - We can include `b` as an extra column and follow it through elimination

> Notice again that word "acts." This is essential. Matrices do something! The matrix `A` acts on `x` to produce `b`. The matrix `E` operates on `A` to give `EA`. The whole process of elimination is a sequence of row operations, alias matrix multiplication.
