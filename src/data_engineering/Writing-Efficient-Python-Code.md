# Writing Efficient Python Code

## Foundations for efficiencies
- Efficient: Fast, Small resource usage
- Writing readable and pythonic code

### Numpy
- Alternative to list
- Homogeneous: must contains same type
- Broadcasting: vectorize operations
- Boolean mask indexing

## Timing and profiling code

### Examining runtime
- %timeit
-  `a = {}` is faster than `a = dict()`

### Code profiling and memory usage
- detailed stats on frequency and duration of function calls
- `line_profiler` and `memory_profiler`

## Efficiencies

### combining, counting and iterating
- `Collections` and `itertools`

### NamedTuple
- 튜플에 이름을 붙일 수 있는 튜플의 서브 클래스이다. 이를 사용하면 튜플이 dict와 같이 key 값을 가지게 되며, 튜플이 마치 변경이 불가능한 딕셔너리 처럼 보여진다. 이러한 관점에서 튜플을 단순히 불변 리스트라고만 정리하는 것은 튜플의 여러 속성들을 간과하는 것이다.
- namedtuple은 딕셔너리에 비해 적은 메모리를 사용한다. 두개의 매개변수를 통해 생성 가능한데, 첫 번째 매개변수는 만들어진  namedtuple을 부를 alias를 지정하는 것이다. 두 번째는 공백으로 구분된 문자열이나 리스트가 입력되는데 튜플의 필드명을 의미한다.

```python
from collections import namedtuple
City = namedtuple('City','name country location')
tokyo = City('Tokyo','JP',((35,689),(139.69)))
```

### Set
- `set.intersection`
- `set.difference`
- `set.union`

### Eliminating loops
- Loop is ugly
- Flat is better than nested
- list comprehension, map and numpy
- holistic conversion
	- holistic: 전체적인

### Pandas Optimization
- `df.iterrows`: each row is `pd.Series`
- `df.itertuples`: each row is `NamedTuple` of `Collections`
- `pd.Series` is heavier than `NameTuple`
- `df.apply`take func to apply with 0 for columns, 1 for rows
- Pandas built on Numpy which allow vectorization
	- `baseball_df.apply(lambda row: row['RS']+row['RA'])`: 181 ms
	- `baseball_df['RS'].values + baseball_df['RA'].values`: **96.5 us**
	- `baseball_df['RS'] + baseball_df['RA']`: 899 us
	- `baseball_df.itertuples()`: 23.6 ms
 
 

