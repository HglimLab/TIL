#Datetime Index

```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

from datetime import datetime 

# 2019년 1월 24일
today = datetime(2019,1,24)

# 0시, 0분 디폴트값
today 

# 시,분,초 지정
today = datetime(2019,1,24,13,39)

today

today.day

today.hour

Pandas with Datetime Index

# datetime 객체로 list 생성 예시
dates = [datetime(2019,1,23), datetime(2019,1,24)]

# 인덱스 전환
dt_index = pd.DatetimeIndex(dates)
dt_index

# 랜덤 데이터를 생성하고 인덱스와 함께 DataFrame 만들기
data = np.random.randn(2,2)
cols = ['A','B']
df = pd.DataFrame(data=data, index=dt_index, columns=cols)

df.index

# Latest Date Location
df.index.argmax()
df.index.max()

# Earliest Date Location
df.index.argmin()

df.index.min()
```

