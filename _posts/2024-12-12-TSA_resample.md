---
layout: single
title: "[Pandas] resample 메서드로 특정 기간별 연산하기"
categories: "Pandas"
tags: ["resample", "TSA", "Pandas"]

toc: true
toc_sticky: true
---

<head>
  <style>
    table.dataframe {
      white-space: normal;
      width: 100%;
      height: 240px;
      display: block;
      overflow: auto;
      font-family: Arial, sans-serif;
      font-size: 0.9rem;
      line-height: 20px;
      text-align: center;
      border: 0px !important;
    }

    table.dataframe th {
      text-align: center;
      font-weight: bold;
      padding: 8px;
    }

    table.dataframe td {
      text-align: center;
      padding: 8px;
    }

    table.dataframe tr:hover {
      background: #b8d1f3; 
    }

    .output_prompt {
      overflow: auto;
      font-size: 0.9rem;
      line-height: 1.45;
      border-radius: 0.3rem;
      -webkit-overflow-scrolling: touch;
      padding: 0.8rem;
      margin-top: 0;
      margin-bottom: 15px;
      font: 1rem Consolas, "Liberation Mono", Menlo, Courier, monospace;
      color: $code-text-color;
      border: solid 1px $border-color;
      border-radius: 0.3rem;
      word-break: normal;
      white-space: pre;
    }

  .dataframe tbody tr th:only-of-type {
      vertical-align: middle;
  }

  .dataframe tbody tr th {
      vertical-align: top;
  }

  .dataframe thead th {
      text-align: center !important;
      padding: 8px;
  }

  .page__content p {
      margin: 0 0 0px !important;
  }

  .page__content p > strong {
    font-size: 0.8rem !important;
  }

  </style>
</head>

## resample 메서드
resample() 메서드는 날짜가 인덱스로 지정되어 있을 때, 특정 기간을 묶어 연산을 한다. 일반적인 데이터프레임에서 groupby 연산과 유사하다. 주별, 월별, 연도별 합계, 평균 등을 계산할 때 유용하다. 설정한 기간 간격 중 마지막 날을 기준으로 연산 결과가 출력된다.


```python
import pandas as pd

# 임의의 데이터 7일 간격으로 12개 만들기
index = pd.date_range('1/1/2024', periods=12, freq='1W')
price = [20, 25, 20, 24, 20, 21, 20, 18, 25, 22, 20, 19]
volume = [10000, 12000, 15000, 11000, 13000, 15000, 10000, 9000, 12000, 10000, 8000, 9000]

df = pd.DataFrame(
    {'Date' : index,
     'Price' : price,
     'Volume' : volume}) 

# 날짜정보를 index로 설정
df = df.set_index('Date')
```


```python
df
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
      <th>Price</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2024-01-07</th>
      <td>20</td>
      <td>10000</td>
    </tr>
    <tr>
      <th>2024-01-14</th>
      <td>25</td>
      <td>12000</td>
    </tr>
    <tr>
      <th>2024-01-21</th>
      <td>20</td>
      <td>15000</td>
    </tr>
    <tr>
      <th>2024-01-28</th>
      <td>24</td>
      <td>11000</td>
    </tr>
    <tr>
      <th>2024-02-04</th>
      <td>20</td>
      <td>13000</td>
    </tr>
    <tr>
      <th>2024-02-11</th>
      <td>21</td>
      <td>15000</td>
    </tr>
    <tr>
      <th>2024-02-18</th>
      <td>20</td>
      <td>10000</td>
    </tr>
    <tr>
      <th>2024-02-25</th>
      <td>18</td>
      <td>9000</td>
    </tr>
    <tr>
      <th>2024-03-03</th>
      <td>25</td>
      <td>12000</td>
    </tr>
    <tr>
      <th>2024-03-10</th>
      <td>22</td>
      <td>10000</td>
    </tr>
    <tr>
      <th>2024-03-17</th>
      <td>20</td>
      <td>8000</td>
    </tr>
    <tr>
      <th>2024-03-24</th>
      <td>19</td>
      <td>9000</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 인덱스를 datetime index로 설정
df.index = pd.to_datetime(df.index)
```


```python
df.index
```

<pre>
DatetimeIndex(['2024-01-07', '2024-01-14', '2024-01-21', '2024-01-28',
               '2024-02-04', '2024-02-11', '2024-02-18', '2024-02-25',
               '2024-03-03', '2024-03-10', '2024-03-17', '2024-03-24'],
              dtype='datetime64[ns]', name='Date', freq=None)
</pre>


resample 메서드를 이용해 월별 평균값을 구해보자.  

```python
# 월별 평균
df.resample(rule='1m').mean()
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
      <th>Price</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2024-01-31</th>
      <td>22.25</td>
      <td>12000.0</td>
    </tr>
    <tr>
      <th>2024-02-29</th>
      <td>19.75</td>
      <td>11750.0</td>
    </tr>
    <tr>
      <th>2024-03-31</th>
      <td>21.50</td>
      <td>9750.0</td>
    </tr>
  </tbody>
</table>
</div>



월별 평균을 계산하면, 매월 마지막 날을 기준으로 평균값이 들어가있다.
<br />

rule에 전달할 인수는 별칭(alias)를 사용할 수도 있다. [Pandas의 공식문서](https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html#dateoffset-objects)를 확인해보면 빈번히 사용되는 dateoffset이 간단한 약어로 설정되어 있다. 



```python
# 월별 평균
df.resample(rule='M').mean()
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
      <th>Price</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2024-01-31</th>
      <td>22.25</td>
      <td>12000.0</td>
    </tr>
    <tr>
      <th>2024-02-29</th>
      <td>19.75</td>
      <td>11750.0</td>
    </tr>
    <tr>
      <th>2024-03-31</th>
      <td>21.50</td>
      <td>9750.0</td>
    </tr>
  </tbody>
</table>
</div>

