# Random Forest

## Hyperparameter Tuning
### max depth
- 나무의 최대 깊이, Node가 늘어나지만 그만큼 과적함의 위험이 증가
- Scikit-Learn: The maximum depth of the tree. If None, then nodes are expanded until all leaves are pure or until all leaves contain less than min-samples-split samples.

### min sample split
- Node가 포함하는 observation의 최소 클래스의 수
	- If min sample split == 2, 노드는 하나의 클래스만 담을 때까지 split
	- if min sample split >2, 하나의 노드에 서로 다른 클래스의 observation이 담길 수 있음
-  min sample split을 증가시키면 무한 가지치기를 제한함으로써 과적합을 예방
- Scikit-Learn: The minimum number of samples required to split an internal node

### max leaf nodes
- 최대 leaf 노드 개수
- 숫자가 작을 시 과소적합의 위험이 있음

### min sample leaf
- leaf 노드가 가져야 할 최소 observation 개수

### n estimator
- Forest의 Tree 개수

### max sample
- 하나의 tree에게 주어지는 data 개수
- 각 Tree에 전체 데이터를 제공한다고 해서 성능이 계속 높아지지 않음
- 일정 수의 data가 충족되면 bootstrap sample fraction 값이 작더라도 성능의 최대치에 도달

### max feature
- split시에 고려하는 feature의 개수

## Referencese
- [Random Forest Hyperparameter Tuning in Python | Machine learning](https://www.analyticsvidhya.com/blog/2020/03/beginners-guide-random-forest-hyperparameter-tuning/)
