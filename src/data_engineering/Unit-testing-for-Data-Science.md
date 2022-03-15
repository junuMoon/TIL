# Unit testing for Data Science

## Unit test

> 유닛 테스트(unit test)는 컴퓨터 프로그래밍에서 소스 코드의 특정 모듈이 의도된 대로 정확히 작동하는지 검증하는 절차다. 즉, 모든 함수와 메소드에 대한 테스트 케이스(Test case)를 작성하는 절차를 말한다. 이를 통해서 언제라도 코드 변경으로 인해 문제가 발생할 경우, 단시간 내에 이를 파악하고 바로 잡을 수 있도록 해준다. 이상적으로, 각 테스트 케이스는 서로 분리되어야 한다. 이를 위해 가짜 객체(Mock object)를 생성하는 것도 좋은 방법이다. 유닛 테스트는 (일반적인 테스트와 달리) 개발자(developer) 뿐만 아니라 보다 더 심도있는 테스트를 위해 테스터(tester)에 의해 수행되기도 한다.

- Benefits
	- time saving
	- trust(code coverage)
	- readibility
	- safety(reduced downtime)

## Writing tests

### Assert statement

- Include a message with assert statements
- Print values of any variable that is relevant to debugging
	- Personally, `import pdb; pdb.set_trace()` is better way to debug
- Beware of using equal assertion to `float` data
	- Instead, use `pytest.approx()`
- Do not use `var == None`, instead use `var is None`
	- PEP-8: Comparisons to singletons like None should always be done with is or is not, never the equality operators.
	- The main advantages I see are emphasizing the explicit desire to compare identity to a builtin, and the inability to break the comparison by defining `__eq__` on arbitrary objects.
	- Equality vs. identity is the difference between those language constructs, and they should absolutely be used that way.
	- [link](https://softwareengineering.stackexchange.com/questions/321861/var-is-none-vs-var-none)

### Exception handling

- If function raises expected error, test will pass
- If function raises non-expected error, test will fail
- If function doesn't raise expected error, test will fail

```python
with pytest.raises(ValueError) as exception_info:  # expected error: ValueError
	foo(bar)
	# If ValueError isn't raised or other errors raised, test will faill
````

### Arguments

- Check all three types of arguments: Bad argument, Normal argument, Special argument
- Bad arguments passed, check the function raises the expected exception
- Special arguments
	- Boundary values: arguments that makes behavior change from raising error to processing as expected
	- Values with which function uses special logic
- Normal arguments: anything that is not a bad or special argument
- Caveat: Not all functions have bad or special arguments

## Test Driven Development

- Unit tests cannot be deprioritized, so that TDD alters the usual function implementing cycle
- Step1
	1. Write unit tests and fix requirements
	2. Run tests and watch it fail
	3. Implement function and run tests again




