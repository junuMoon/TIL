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
- Step
	1. Write unit tests and fix requirements
	2. Run tests and watch it fail
	3. Implement function and run tests again

## Organizing porject


### Directory structure

```
data/
|-- raw/
|	|-- raw_data-20210101.csv
|-- clean/
|	|-- clean_data-20210101.csv
src/
|-- data/
|	|-- __init__.py
|	|-- preprocessing_helpers.py
|-- features/
|	|-- __init__.py
|	|-- as_numpy.py
|-- models/
|	|-- __init__.py
|	|-- train.py
|-- visualization/
|	|-- __init__.py
|	|-- plots.py
tests/
|-- data/
|	|-- __init__.py
|	|-- test_preprocessing_helpers.py
|-- features/
|	|-- __init__.py
|	|-- test_as_numpy.py
|-- models/
|	|-- __init__.py
|	|-- test_train.py
```

### Test class

- Test class is a container for a single unit's test
- Create a class for each function to get tested

```python
from model.filename import function_name

class TestFunctionName:
	def test_with_normal_argument(self):
		...

	def test_with_special_argument(self):
		...

	def test_with_bad_argument(self):
		...
```

### Running tests

- using node ID: `pytest <path to test module>::<test class name>::<unit test name>`
- using keyword: `pytest -k <keyword>`
	- allows logical operator: and, not ...

### Handling failures

- Tests to be expected to fail use `pytest.mark.xfail`
	- `@pytest.mark.xfail(reason=train_model() is not implmented)`
- Tests to be expected to fail in specific conditions use `@pytest.mark.skipif(boolean_expression)`
	- `@pytest.mark.skipif(sys.version_info > (2, 7), reason='requires Python version lower than or equal to 2.7)`
- option `-r` show reason for skipping

### Continuous Integration using Travis CI

1. Create a configuration file(`.travis.yml`)
2. Push the file to github
3. Install the Travis CI app
4. Add install and after_success setting to config file

#### Code coverage

code coverage = num lines of application code that ran during testing / total num lines of application code

#### .travis.yml

```yml
language: python
python:
	- "3.6"
install:
	- pip install -e .
	- pip install pytest-cov codecov
script:
	- pytest tests
	- pytest --cov=src tests
after_success:
	- codecov
```

> If you install your project with an -e flag (e.g. pip install -e mynumpy) and use it in your code (e.g. from mynumpy import some_function), when you make any change to some_function, you should be able to use the updated function without reinstalling it.

## Testing Models, Plots and Much More

### Setup & Teardown using Fixture

- Step:
	1. Setup environment
	2. Call the function
	3. Assert statement
	4. Teardown environment
- Fixture(`@pytest.fixture`)
	- A function to be used as test environment
	- Uses `yield` for teardown step
	- Remain section runs only when the test has finished executing
	- `tmpdir`: a built-in pytest fixture that creates a temporary directory during test

#### Test

```python

def test_on_raw_data(raw_and_clean_data_file):
	raw_path, clean_path = raw_and_clean_data_file
	preprocess(raw_path, clean_path)
	with open(clean_path) as f:
		data = f.readlines()
	assert data[0] = 'hi'
```

#### Fixture

```python
@pytest.fixture
def raw_and_clean_data_file(tmpdir):
	raw_path = Path(tmpdir.join('raw.txt'))
	clean_path = Path(tmpdir.join('clean.text'))
	with raw_path.open('w') as f:
		f.write('hello')
	
	yield raw_path, clean_path

	# After the test is finished, teardown step runs
	# Using tmpdir, no teardown code is necessary
	# raw_path.unlink()
	# clean_path.unlink()
```

### Mocking

Mocking is to replace potentially buggy dependencies(functions, libraries etc) during testing to run unit tests independently and bug-free

### Testing Models

- Check the model works as expected in different dataset
	- Use dataset where reutrn value is known(simple linear data)
	- Use inequalities(circular data)
- Model Performance
	- appropirate metrics for the task of models

---
[repo](https://github.com/gutfeeling/)









