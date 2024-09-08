{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "데이터 값을 특정 구간으로 분할하고 정렬해야 할 때 cut을 사용한다. 이 함수는 연속 변수에서 범주형 변수로 이동하는 데에도 유용하다. 예를 들어, cut은 연령을 연령대 그룹으로 변환할 수 있다.  \n",
    "\n",
    "**cut(array, bins, labels)**\n",
    "\n",
    "- array: 나누고자 하는 배열\n",
    "- bins: 나누고자 하는 구간 수, array의 최소값과 최대값을 포함하도록 양쪽에서 0.1%씩 확장된다.\n",
    "- labels: 구간별 이름\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[(0.994, 3.0], (5.0, 7.0], (3.0, 5.0], (3.0, 5.0], (5.0, 7.0], (0.994, 3.0]]\n",
       "Categories (3, interval[float64, right]): [(0.994, 3.0] < (3.0, 5.0] < (5.0, 7.0]]"
      ]
     },
     "execution_count": 1,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "import pandas as pd\n",
    "import numpy as np\n",
    "\n",
    "pd.cut(np.array([1, 7, 5, 4, 6, 3]), 3) #3개의 구간으로 구분"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "최소값인 1을 포함하기 위해 첫번째 구간은 0.994부터 시작한다.    \n",
    "예를 들어 시험성적의 분포가 57점부터 100까지 점수가 분포하고 이를 상대평가하여 A부터 E까지 5개의 등급으로 나눠보자."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[(56.957, 65.6], (74.2, 82.8], (56.957, 65.6], (82.8, 91.4], (91.4, 100.0], (65.6, 74.2], (82.8, 91.4], (91.4, 100.0]]\n",
       "Categories (5, interval[float64, right]): [(56.957, 65.6] < (65.6, 74.2] < (74.2, 82.8] < (82.8, 91.4] < (91.4, 100.0]]"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "score = np.array([57, 78, 64, 83, 95, 72, 89, 100])\n",
    "interval = pd.cut(score, 5)\n",
    "interval"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "describe() 메서드를 사용하면 구간별 빈도와 비율을 확인할 수 있다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>counts</th>\n",
       "      <th>freqs</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>categories</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>(56.957, 65.6]</th>\n",
       "      <td>2</td>\n",
       "      <td>0.250</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>(65.6, 74.2]</th>\n",
       "      <td>1</td>\n",
       "      <td>0.125</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>(74.2, 82.8]</th>\n",
       "      <td>1</td>\n",
       "      <td>0.125</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>(82.8, 91.4]</th>\n",
       "      <td>2</td>\n",
       "      <td>0.250</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>(91.4, 100.0]</th>\n",
       "      <td>2</td>\n",
       "      <td>0.250</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                counts  freqs\n",
       "categories                   \n",
       "(56.957, 65.6]       2  0.250\n",
       "(65.6, 74.2]         1  0.125\n",
       "(74.2, 82.8]         1  0.125\n",
       "(82.8, 91.4]         2  0.250\n",
       "(91.4, 100.0]        2  0.250"
      ]
     },
     "execution_count": 9,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "interval.describe()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "labels를 이용하면 구간별로 이름을 붙일 수 있다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "['A', 'C', 'A', 'D', 'E', 'B', 'D', 'E']\n",
       "Categories (5, object): ['A' < 'B' < 'C' < 'D' < 'E']"
      ]
     },
     "execution_count": 14,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "label = pd.cut(score, 5, labels=['A','B','C','D','E'])\n",
    "label"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "handson",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.8.19"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}
