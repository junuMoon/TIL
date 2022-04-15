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
