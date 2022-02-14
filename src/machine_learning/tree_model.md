# Random Forest

## Ensemble

단일 모델이 아닌 여러 개의 모델을 생성하여 예측을 결합하여 더 정확한 예측을 도출하는 방법. 랜덤포레스트는 Bagging 기법을 사용.

### Bagging

- Bootstrap AGGregatING: Bootstrap으로 학습한 여러 개의 tree를 생성하여 각 모델의 결과를 집계하여 예측
- Bootstrap: 전체 데이터에서 무작위 복원 추출로 데이터 샘플을 수집하여 각 Tree를 학습
- Aggregating(Voting): 다수의 모델의 결과를 다수결(voting)의 방식으로 결정
- Bagging 기법은 데이터의 높은 분산으로 인한 Overfitting 문제를 샘플링으로 완화하여 Random Forest가 좀 더 general, robust하게 만듬

### Boosting: 

- Bagging과 동일하게 복원 랜덤 샘플링
- 각 모델마다 가중치를 부여하여 순차적(Sequential)하게 학습
- Random Forest가 각 모델을 병렬적(Parallel)하게 학습하는 것과 반대
- 오답에 대해 높은 가중치를 부여하여 다음 모델이 이를 해결하게 할 수 있도록 함
	- 맞추지 못한 데이터를 포함하여 다시 표본 추출 (sampling with weight on error)
- RandomForest보다 좀 더 specific한 모델이 됨

## Feature Importance

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
- https://swalloow.github.io/bagging-boosting/
- https://velog.io/@guns/머신러닝-스터디-앙상블-Bagging-Random-Forest