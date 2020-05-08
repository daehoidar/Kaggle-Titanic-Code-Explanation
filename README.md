# Kaggle-Titanic-Code-Explanation<br/>
##### 이유한님 영상 참고했습니다.
<br/>

```python 
import numpy as np
```
numerical python의 줄임말로,  수치적인 해석, 연산, 방법에 관한 라이브러리<br/><br/>


```python
import pandas as pd
```
데이터 프레임을 쉽게 다룰 수 있게 해주는 많은 함수들이 포함된 라이브러리<br/><br/>


```python
import matplotlib.pyplot as plt
import seaborn as sns
```
데이터 시각화<br/><br/>


```python
plt.style.use('seaborn')
```
matplotlib 라이브러리를 seaborn 스타일로 사용<br/><br/>


```python
sns.set(font_scale=2.5)
```
폰트 사이즈를 미리 지정하여 후에 일일이 그래프의 폰트의 사이즈를 지정하지 않아도 되고 통일성 있음<br/><br/>


```python
import missingno as msno
```
데이터셋의 null 데이터를 쉽게 보여줌<br/><br/>


```python
import warnings
warnings.filterwarnings('ignore')
```
워닝 무시<br/><br/>


```python
%matplotlib inline
```
matplotlib의 그래프를 새로운 창에 띄우지 않고 노트에서 바로 불 수 있게 함<br/><br/>

---


