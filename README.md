# Kaggle-Titanic-Code-Explanation<br/>
##### 이유한님 영상 참고했습니다.<br/>

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
matplotlib 라이브러리를 seaborn 스타일로 사용.<br/><br/>


```python
sns.set(font_scale=2.5)
```
폰트 사이즈를 미리 지정하여 후에 일일이 그래프의 폰트의 사이즈를 지정하지 않아도 되고 통일성 있다.<br/><br/>


```python
import missingno as msno
```
데이터셋의 null 데이터를 쉽게 보여준다.<br/><br/>


```python
import warnings
warnings.filterwarnings('ignore')
```
워닝 무시<br/><br/>


```python
%matplotlib inline
```
matplotlib의 그래프를 새로운 창에 띄우지 않고 노트에서 바로 불 수 있게 한다.<br/><br/>

```python
d_train = pd.read_csv('../input/titanic/train.csv')
d_test = pd.read_csv('../input/titanic/test.csv')
```
```python
d_train.head(10)
```
컬럼 이름만 봤을 때는 사람 이름과 티켓은 생존과 연관이 적을 것 같은 느낌이 든다.<br/><br/>

```python
type(d_train)
```
```python
d_train.shape
```
컬럼이 12개인 것을 확인할 수 있다.<br/><br/>

```python
d_train.columns
```

```python
d_train.describe()
```
```python
d_test.describe()
```
위의 코드처럼 칼럼별로 다양한 수치를 보는 것도 가능하다.<br/><br/>

```python
d_train['Age'].isnull().sum() / d_train['Age'].shape[0]
```
Age의 전체 데이터에 대한 null데이터 수 구한다.<br/><br/>

```python
for col in d_train.columns:
    msg = 'column: {:>10}\t Percent of NaN vlaue: {:.2f}%'.format(col, 100 * (d_train[col].isnull().sum() / d_train[col].shape[0]))
    print(msg)
```
같은 방식으로 칼럼별로 null데이터 수에 전체 데이터 수 나눠서 null 데이터의 비율을 구한다.<br/>
>: 오른쪽으로 정렬, M: 왼쪽 정렬, 무입력: 정렬 안 함<br/><br/>

```python
for col in d_test.columns:
    msg = 'column: {:>10}\t Percent of NaN vlaue: {:.2f}%'.format(col, 100 * (d_test[col].isnull().sum() / d_test[col].shape[0]))
    print(msg)
```
test 데이터도 null 데이터 비율을 확인해 본다.<br/><br/>

```python
d_train[col].isnull() 
```
null값이면 true를 리턴하고 null이 아니면 false를 리턴한다.<br/><br/>

```python
d_train.isnull().sum()
```
true는 1, false는 0으로 취급한다. 값이 1인 true만 합하여 결측치의 수를 확인할 수 있다.<br/><br/>

```python
d_train.iloc[4:20, 4]
```
something.iloc[몇 번째부터 몇 번째 데이터까지 볼 것인지 정함, 몇 번째 칼럼 볼 것인지 정함](인덱싱 사용)<br/><br/>

```python
msno.matrix(df = d_train.iloc[:, :], figsize = (8, 8), color = (0.2, 0.6, 0.5))
```
d_train.iloc[:, :]위에서 설명<br/>
figsize: 가로 세로 크기<br/>
color: 왼쪽부터 RGB 그래프 색 설정<br/>
비어보이는 칸이 null데이터가 있는 칸을 뜻.<br/><br/>

```python
msno.bar(df = d_train.iloc[:, :], figsize = (8, 8), color = (0.2, 0.6, 0.5))
```
막대 그래프 형태로도 결측치 확인이 가능하다.<br/><br/>

```python
d_train['Survived'].value_counts().plot()
```
plt.plot(d_train['Survived'].value_counts())와 같은 의미이다.<br/><br/>

```python
d_train['Survived'].value_counts().plot.pie(explode=[0, 0.1], autopct = '%1.1f%%', shadow = True, figsize = (6, 6))
```

```python
f, ax = plt.subplots(1, 2, figsize = (18, 8))
# f, ax = plt.subplots(행(로우), 열(칼럼), figsize = (가로 사이즈, 세로 사이즈))


d_train['Survived'].value_counts().plot.pie(explode=[0, 0.1], autopct = '%1.1f%%', ax = ax[0], shadow = True)
# d_train['Survived'].value_counts(): survived 칼럼의 값들을 종류별로 카운트함. Series타. Series는 plot을 갖고 있음.
# .pie: 원 그래프 형태로 나타냄.
# explode=[0, 0.1]: 보기 쉽게 그래프의 다른 값을 떨어뜨려 나타냄.
# autopct = '%1.1f%%': 퍼센트 수치를 나타냄.
# ax = ax[0]: 앞서 선언한 열 두 개 중 앞에 것에 해당한다는 것을 뜻함.
# shadow = True: 그림자를 표시하겠다는 것 뜻함.

ax[0].set_title('Pie plot - Survived')
# 첫 번째 그래프의 타이틀을 달아줌.

ax[0].set_ylabel('')
# y레이블 설정. (아무것도 입력하지 않음)


sns.countplot('Survived', data = d_train, ax = ax[1])
# seborn 라이브러리를 이용하여 카운트 해주는 플롯인 countplot을 사용. 
# countplot은 첫 번째로 칼럼의 이름('Survived')을 인풋 받고, 그 다음
# data = d_train: 데이터는 d_train을 쓰기로 지정.
# ax = ax[1]: 만든 두 칼럼 중 두 번째 칼럼에 해당.


ax[1].set_title('Count plot - Survived')
# 두 번째 그래프의 타이틀을 달아줌.

plt.show()
# plt그래프 보여줌.
```
죽은 사람과 생존한 사람의 비율이 극단적이게 한 쪽이 많지 않고 적절한 비율인 것을 확인 가능하다.<br/><br/>
### 1. Pclass<br/>
Pclass와 생존률의 관계를 확인하려 한다.
```python
d_train[['Pclass', 'Survived']].groupby(['Pclass'], as_index = True).count()
# pclass와 Survived를 나타내되 Pclass로 그룹화한다.
# .count()는 Pclass별로 Survived데이터가 몇 개 존재하는지 보여준다.
```
mysql이랑 비슷한 것 같다.<br/><br/>

```python
d_train[['Pclass', 'Survived']].groupby(['Pclass']).sum()
```
sum은 Pclass별로 Survived(사망:0, 생존:1)의 합이니까 산 사람의 수를 나타낸다고 해석할 수 있다.<br/><br/>

```python
d_train[['Pclass', 'Survived']].groupby(['Pclass']).mean()
```
평균을 구하는 mean을 이용하여 생존률도 확인한다.<br/><br/>

```python
d_train['Survived'].unique()
```

```python
pd.crosstab(d_train['Pclass'], d_train['Survived'], margins = True).style.background_gradient(cmap='Purples')
```
margins 이 True면 all보여주고 False면 보여주지 않음, cmap ='색 종류'<br/><br/>

```python

```
```python

```
