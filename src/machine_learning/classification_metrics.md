# Classificaiton Metrics

## Confusion Matrix(혼동행렬)

모델이 내놓은 답과 실제 정답을 2x2 매트릭스로 나타낸 것
- True Positive(TP) : 실제 True인 정답을 True라고 예측 (정답)
- False Positive(FP) : 실제 False인 정답을 True라고 예측 (오답)
- False Negative(FN) : 실제 True인 정답을 False라고 예측 (오답)
- True Negative(TN) : 실제 False인 정답을 False라고 예측 (정답)

이를 바탕으로 Precision(정밀도), Recall(재현율), F1-Score 등을 계산할 수 있음

## Precision

- 정밀도: TP / TP + FP
- 모델이 True라고 한 것 중 실제 True의 비율
- FN보다 FP가 중요한 경우 사용
- 모델의 목적이 하나라도 더 맞추는 것일 때 재현율이 중요(i, g. 스팸메일)

## Recall

- 재현율: TP / TP + FN
- 실제 True 중 모델이 True라고 한 것의 비율
- FP보다 FN가 중요한 경우 사용
- 모델의 목적이 하나라도 놓치지 않는 것일 때 재현율이 중요(i, g. 암 판별)

## Trade-off of Precision and Recall
- 모델이 True라고 예측하는 확률값의 임계값(Threshold)에 따라 정밀도와 재현율은 Trade-off 관계가 정해진다. 
- 임계값을 0.5 이하로 낮추면 모델이 더 많이 True라고 예측 -> 재현율(Recall)이 올라감
- 임계값을 0.5 이상으로 올리면 모델이 더 많이 False라고 예측 -> 정밀도(Precision)이 올라감
- Threshold: 0.1 -> Precision: 0.3, Recall: 1
- Threshold: 1 -> Precision: 1, Recall: 0.06


## Reference
- https://sumniya.tistory.com/26
- https://en.wikipedia.org/wiki/Decision_tree_learning
