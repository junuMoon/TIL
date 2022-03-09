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
 
 

