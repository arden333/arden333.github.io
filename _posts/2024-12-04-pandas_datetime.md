---
layout: single
title: "[Pandas] datetime으로 날짜 데이터 생성, 활용하는 방법"
categories: "Pandas"
tags: ["datetime", "Pandas"]

toc: true
toc_sticky: true
---

## 파이썬에서 날짜 데이터 다루는 방법
대부분의 데이터셋에는 날짜 데이터가 있다. python에서 날짜 데이터는 Numpy와 Pandas를 이용해 생성하고 활용할 수 있다. 
이 포스팅에서는 Pandas에서 날짜 데이터를 다루는 방법에 대해 집중적으로 알아보고자 한다.

## Pandas
### datetime 라이브러리 활용
datetime 라이브러리를 이용하면 쉽게 날짜 데이터를 처리할 수 있다.
<br />
```python
from datetime import datetime
```
<br />
그럼 날짜를 생성해보자. 2024년 12월 4일 14시 30분에 대한 날짜 데이터를 생성하려고 한다.
<br />
```python
year = 2024
month = 12
day = 4
hour = 14
min = 30
```
<br />
위의 각 변수들은 시간 데이터가 아닌 숫자일 뿐이다. datetime 라이브러리를 활용해보자. datetime의 각 인수는 순서대로 '연도, 월, 일, 시간, 분'이다.
나노초(ns) 단위까지 설정가능 하며, 설정하지 않는다면 default 값은 0이다.
<br />
```python
my_date = datetime(year, month, day, hour, min)
my_date # datetime.datetime(2024, 12, 4, 14, 30)
```
<br />
날짜 데이터에서 월 또는 연도만 추출하고 싶다면 아래와 같이 하면 된다.
<br />
```python
my_date.year # 2024
my_date.month # 12
```
<br />
### datetime을 index로 활용하기
time series 데이터를 다룰 때는 주로 날짜, 시간 데이터를 인덱스로 설정해서 사용한다. Pandas는 datetime index를 생성할 수 있는 메서드를 제공한다.
<br />
```python
import pandas as pd

idx = pd.date_range('7/8/2018', periods=7, freq='D') #7개 간격, 빈도는 D(day, 일) 기준
idx
# DatetimeIndex(['2018-07-08', '2018-07-09', '2018-07-10', '2018-07-11',
              '2018-07-12', '2018-07-13', '2018-07-14'],
              dtype='datetime64[ns]', freq='D')
```
<br />
datetime index를 이용해 쉽게 최근 날짜가 가장 오래된 날짜를 찾을 수도 있다.
<br />
```python
idx.max() # Timestamp('2018-07-14 00:00:00')
idx.min() # Timestamp('2018-07-08 00:00:00')
```
<br />


## Numpy
Numpy를 활용해서 날짜 데이터의 array(배열)를 만들 수도 있다. 

### 날짜 배열 만들기
<br />
```python
import numpy as np

np.array(['2016-03-15', '2017-05-24', '2018-08-09'], dtype='datetime64')
# array(['2016-03-15', '2017-05-24', '2018-08-09'], dtype='datetime64[D]')
```
<br />
numpy에서 배열을 생성할 때 dtype을 `datetime64`로 설정하지 않으면 그냥 텍스트로 인식한다. 데이터 유형을 날짜로 설정하기 위해서 설정해주어야 한다.
그러면 만들어진 array의 데이터타입이 `datetime64[D]`로 나온다. '[D]'는 날짜 데이터가 구현된 정밀도 수준을 의미한다. 즉, 일 단위까지 값이 있다는 의미이다.
<br />
이를 활용해 배열을 만들 때 정밀도 수준을 조정할 수도 있다. '2016-30-15'에서 연도만 추출해 배열로 만들고 싶을 경우, 데이터타입을 `datetime[Y]`로 설정해주면 된다.
<br />
```python
np.array(['2016-03-15', '2017-05-24', '2018-08-09'], dtype='datetime64[Y]')
# array(['2016', '2017', '2018'], dtype='datetime64[Y]')
```
<br />
## 일정한 간격의 날짜 배열 만들기
`np.arange`를 이용해 시작일자와 종료일자 사이의 일정한 간격의 날짜 데이터를 만들 수도 있다. 
아래의 코드는 6월 1일부터 23일까지 7일 간격의 배열을 만든다는 것을 의미한다.
이 때 주의할 점은 간격이 시작일, 종료일의 범위와 맞아야 한다는 것이다. 아래의 경우 간격을 7년으로 설정할 경우 오류가 난다.
<br />
```python
np.arange('2018-06-01', '2018-06-23', 7, dtype='datetime64[D]')
# array(['2018-06-01', '2018-06-08', '2018-06-15', '2018-06-22'], dtype='datetime64[D]')
```
<br />
