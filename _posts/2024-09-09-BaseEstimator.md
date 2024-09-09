---
layout: single
title: "[Sklearn] BaseEstimator"
categories: "Sklearn"
tags: "BaseEstimator"

toc: true
toc_sticky: true
---

## BaseEstimator란?
BaseEstimator는 사이킷런에서 모든 추정기(estimator)의 기반 클리스이다. 추정기란 모델을 학습하고 예측할 수 있는 객체를 말한다. BaseEstimator는 이 추정기들의 공통적인 기능을 정의하는 클래스이다. BaseEstimator는 직접 사용되는 클래스는 아니며 주로 새로운 사용자 정의 모델을 만들 때 상속하여 기본 기능을 사용할 수 있게 해준다.

## BaseEstimator의 주요 역할
- 초기화된 하이퍼파라미터 관리: BaseEstimator는 모델이 생성될 때 설정되는 하이퍼파라미터들을 저장하고, 이를 나중에
 쉽게 접근할 수 있도록 한다
- **get_params()** 메서드 제공: 추정기의 하이퍼파라미터를 딕셔너리로 반환
- **set_params()** 메서드 제공: 주어진 하이퍼파라미터로 추정기의 속성을 설정

## BaseEstimator 예시
```python
from sklearn.base import BaseEstimator, ClassifierMixin
import numpy as np

# 사용자 정의 분류기 정의
class SimpleClassifier(BaseEstimator, ClassifierMixin):
    def __init__(self, threshold=0.5):
        # 하이퍼파라미터로 threshold를 받음
        self.threshold = threshold

    def fit(self, X, y):
        # fit 메서드에서는 단순히 X의 평균을 계산하여 저장함
        self.mean_ = np.mean(X, axis=0)
        return self  # fit 메서드는 자기 자신을 반환해야 함

    def predict(self, X):
        # X의 평균값과 학습한 평균값(mean_)을 비교하여 예측
        return (np.mean(X, axis=1) > self.threshold).astype(int)

    def score(self, X, y):
        # 간단한 정확도 계산
        predictions = self.predict(X)
        return np.mean(predictions == y)

# 간단한 데이터셋 생성
X = np.array([[1, 2], [2, 3], [3, 4], [4, 5]])
y = np.array([0, 0, 1, 1])

# 사용자 정의 분류기 사용
clf = SimpleClassifier(threshold=2.5)
clf.fit(X, y)
predictions = clf.predict(X)

print("예측값:", predictions)
print("정확도:", clf.score(X, y))
```

    예측값: [0 0 1 1]
    정확도: 1.0


메서드를 사용하는 방법은 다음과 같다.

```python
# 하이퍼파라미터 가져오기
print("초기 하이퍼파라미터:", clf.get_params())

# 하이퍼파라미터 설정하기
clf.set_params(threshold=3.0)
print("수정된 하이퍼파라미터:", clf.get_params())
```

    초기 하이퍼파라미터: {'threshold': 2.5}
    수정된 하이퍼파라미터: {'threshold': 3.0}

