---
layout: single
title: "[Pandas] cut"
categories: "Pandas"
tags: "cut"

toc: true
toc_sticky: true
---

## cut 용도
데이터 값을 특정 구간으로 분할하고 정렬해야 할 때 cut을 사용한다. 이 함수는 연속 변수에서 범주형 변수로 이동하는 데에도 유용하다. 예를 들어, cut은 연령을 연령대 그룹으로 변환할 수 있다.  

## cut 구성
**cut(array, bins, labels)**

- array: 나누고자 하는 배열
- bins: 나누고자 하는 구간 수, array의 최소값과 최대값을 포함하도록 양쪽에서 0.1%씩 확장된다.
- labels: 구간별 이름

## 예제

```python
import pandas as pd
import numpy as np

pd.cut(np.array([1, 7, 5, 4, 6, 3]), 3) #3개의 구간으로 구분
```




    [(0.994, 3.0], (5.0, 7.0], (3.0, 5.0], (3.0, 5.0], (5.0, 7.0], (0.994, 3.0]]
    Categories (3, interval[float64, right]): [(0.994, 3.0] < (3.0, 5.0] < (5.0, 7.0]]



최소값인 1을 포함하기 위해 첫번째 구간은 0.994부터 시작한다.  

  
예를 들어 시험성적의 분포가 57점부터 100까지 점수가 분포하고 이를 상대평가하여 A부터 E까지 5개의 등급으로 나눠보자.


```python
score = np.array([57, 78, 64, 83, 95, 72, 89, 100])
interval = pd.cut(score, 5)
interval
```




    [(56.957, 65.6], (74.2, 82.8], (56.957, 65.6], (82.8, 91.4], (91.4, 100.0], (65.6, 74.2], (82.8, 91.4], (91.4, 100.0]]
    Categories (5, interval[float64, right]): [(56.957, 65.6] < (65.6, 74.2] < (74.2, 82.8] < (82.8, 91.4] < (91.4, 100.0]]



describe() 메서드를 사용하면 구간별 빈도와 비율을 확인할 수 있다.


```python
interval.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>counts</th>
      <th>freqs</th>
    </tr>
    <tr>
      <th>categories</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>(56.957, 65.6]</th>
      <td>2</td>
      <td>0.250</td>
    </tr>
    <tr>
      <th>(65.6, 74.2]</th>
      <td>1</td>
      <td>0.125</td>
    </tr>
    <tr>
      <th>(74.2, 82.8]</th>
      <td>1</td>
      <td>0.125</td>
    </tr>
    <tr>
      <th>(82.8, 91.4]</th>
      <td>2</td>
      <td>0.250</td>
    </tr>
    <tr>
      <th>(91.4, 100.0]</th>
      <td>2</td>
      <td>0.250</td>
    </tr>
  </tbody>
</table>
</div>



labels를 이용하면 구간별로 이름을 붙일 수 있다.


```python
label = pd.cut(score, 5, labels=['A','B','C','D','E'])
label
```




    ['A', 'C', 'A', 'D', 'E', 'B', 'D', 'E']
    Categories (5, object): ['A' < 'B' < 'C' < 'D' < 'E']


