---
layout: post
title:  "Kaggle-타이타닉 생존자 예측하기(Python) - 01"
date:   2018-07-25
author: EunHye Jung
categories: bigdata
tags: bigdata
cover:  "/assets/instacode.png"
---  

- - -    
     
*이 글은 [참조 사이트](https://campus.datacamp.com/courses/kaggle-python-tutorial-on-machine-learning/getting-started-with-python?ex=1)를 기반으로 이해한 내용을 개인적인 학습을 목적으로 정리한 것이며, 오역이나 잘못된 내용이 있을 수 있습니다.*
   
- - -   


### Get the Data with Pandas  
  
타이타닉 생존 확률을 예측하는데 필요한 트레이닝 셋과 테스트셋을 URL을 이용해서 불러와보자.  
우리는 트레이닝 셋을 모델을 만드는데 사용할 것이고, 테스트셋을 이 모델을 검증하는데 사용할 것이다.  
    
먼저 Pandas 라이브러리를 import 한다음, 트레이닝셋과 테스트셋을 URL을 이용해 불러온다음,  
`.head()` 메소드를 이용해서 몇개의 행들을 데이터 프레임에서 불러와서 확인해보자.   
  
  
```python  
import pandas as pd

train_url = "http://s3.amazonaws.com/assets.datacamp.com/course/Kaggle/train.csv"
train = pd.read_csv(train_url)
train.head(3)

test_url = "http://s3.amazonaws.com/assets.datacamp.com/course/Kaggle/test.csv"
test = pd.read_csv(test_url)
test.head(3)
```   
   
   
- - -   
   
### Understanding Data   
   
실제 데이터 분석을 시작하기 전에, 데이터의 구조를 이해하는 것을 중요하다.  
train, test 데이터가 둘다 데이터 프레임 객체이므로 우리는 `.describe()` 메소드를 이용해서 데이터 프레임에 담긴 데이터들을 탐색해볼 수 있다.   
`.describe()`는 데이터 프레임의 칼럼과 특징들을 요약해준다.   
또한, 평균과 최대값 기타 등등의 정보도 확인가능하다.   
데이터를 탐색하는 또다른 유용한 방법은 `.shape` 속성을 이용해 차원을 확인하는 것이다.   
   
   
```python   
train.shape
# (891, 12)

test.shape
# (418, 11)

train.describe()
#        PassengerId    Survived      Pclass         Age       SibSp  \
# count   891.000000  891.000000  891.000000  714.000000  891.000000   
# mean    446.000000    0.383838    2.308642   29.699118    0.523008   
# std     257.353842    0.486592    0.836071   14.526497    1.102743   
# min       1.000000    0.000000    1.000000    0.420000    0.000000   
# 25%     223.500000    0.000000    2.000000   20.125000    0.000000   
# 50%     446.000000    0.000000    3.000000   28.000000    0.000000   
# 75%     668.500000    1.000000    3.000000   38.000000    1.000000   
# max     891.000000    1.000000    3.000000   80.000000    8.000000   

#             Parch        Fare  
# count  891.000000  891.000000  
# mean     0.381594   32.204208  
# std      0.806057   49.693429  
# min      0.000000    0.000000  
# 25%      0.000000    7.910400  
# 50%      0.000000   14.454200  
# 75%      0.000000   31.000000  
# max      6.000000  512.329200

test.describe()
#        PassengerId    Survived      Pclass         Age       SibSp  \
# count   891.000000  891.000000  891.000000  714.000000  891.000000   
# mean    446.000000    0.383838    2.308642   29.699118    0.523008   
# std     257.353842    0.486592    0.836071   14.526497    1.102743   
# min       1.000000    0.000000    1.000000    0.420000    0.000000   
# 25%     223.500000    0.000000    2.000000   20.125000    0.000000   
# 50%     446.000000    0.000000    3.000000   28.000000    0.000000   
# 75%     668.500000    1.000000    3.000000   38.000000    1.000000   
# max     891.000000    1.000000    3.000000   80.000000    8.000000   

#             Parch        Fare  
# count  891.000000  891.000000  
# mean     0.381594   32.204208  
# std      0.806057   49.693429  
# min      0.000000    0.000000  
# 25%      0.000000    7.910400  
# 50%      0.000000   14.454200  
# 75%      0.000000   31.000000  
# max      6.000000  512.329200

```   
   
   
- - - 
   
   
### Rose Vs Jack, or Female Vs Male     
   
   
트레이닝셋에 "Survived" 칼럼은 생존 여부를 나타낸다.  
얼마나 많은 사람이 타이타닉 재난에서 살아남았는지 확인하고 싶을때, `value_counts()`메소드를 사용하면 된다.  
   
   
```python
print(train["Survived"].value_counts())

# 0    549
# 1    342
# Name: Survived, dtype: int64
```  
  
만약에 `value_count()`메소드에 인자값으로 `normalize=True`를 넣어주면, 생존비율을 확인할 수도 있다.   
   
```python
print(train["Survived"].value_counts(normalize = True))

# 0    0.616162
# 1    0.383838
# Name: Survived, dtype: float64
```    
   
`value_counts()` 메소드를 통해 트레이닝셋 데이터에서 549명(62%)이 죽고 342명(38%)이 산다는 것을 확인할 수 있었다.  
   
타이타닉 영화를 본 사람은 알겠지만 구조보트의 탑승에는 여성과 어린 아이들에게 우선권이 주어진다.  
그럼 성별이 생존여부에 중요한 예측변수가 될 수 있을까?   
   
우리는 `value_counts()`를 사용해서 생존한 남성과 여성에 대한 정보를 비교해볼 수 있다.   
   
우선 남성과 여성의 수가 얼마나 되는지 확인해보자.   
  
```python   
print(train["Sex"].value_counts())
# male      577
# female    314
# Name: Sex, dtype: int64


print(train["Sex"].value_counts(normalize = True))
# 0    0.616162
# 1    0.383838
# Name: Survived, dtype: float64

```   
  
남성 중에 생존한 사람과 죽은 사람이 얼마나 되는지 확인해보자.    
   
```python  
print(train["Survived"][train["Sex"] == 'male'].value_counts())
# male      577
# female    314
# Name: Sex, dtype: int64

print(train["Survived"][train["Sex"] == 'male'].value_counts(normalize = True))
# 0    0.811092
# 1    0.188908
# Name: Survived, dtype: float64
```      
  
남성의 경우 80%가 넘는 인원이 사망한 것을 확인할 수 있다.   
  
이제 여성 중에 생존한 사람과 죽은 사람이 얼마나 되는지 확인해보자.  
   
```python  
print(train["Survived"][train["Sex"] == 'female'].value_counts())
# 1    233
# 0     81
# Name: Survived, dtype: int64

print(train["Survived"][train["Sex"]== 'female'].value_counts(normalize = True))
# 1    0.742038
# 0    0.257962
# Name: Survived, dtype: float64
```   
  
여성의 경우 26%정도의 사람이 죽고, 74%정도 생존한 것을 확인할 수 있다.   
(남성에 비해 여성의 생존확율이 훨씬 높인 것을 확인 할 수 있다)   
    
    
- - -  
    
    
### Does age play a role ?   
    
성별말고, 생존에 영향을 미치는 변수 나이(age)가 될 수 있다.   
먼저 아이들의 경우 생존 가능성이 높다.  
우리는 새로운 범주형 변수인 `Child`를 만들어서 테스트해볼 수 있따.  
`Child`는 나이가 18세보다 작으면 1로 세팅될 것이고, 나이가 18세 이상이면 0으로 세팅될 것이다.   
  
우선 새로운 칼럼 "Child"을 만들고 "NaN"을 할당하자.   
  
````python   
train["Child"] = float('NaN')    
```   
   
승객의 나이가 18세보다 작으면 1을, 18세 이상이면 0을 세팅해보자.   
    
```python   
train["Child"][train["Age"] < 18] = 1
train["Child"][train["Age"] >= 18] = 0
```   
   
   
- - -   
   
    
### First Prediction   
   
   
우리는 테스트셋을 우리가 한 예측을 평가하는데 사용한다.  
트레이닝셋과 달리 테스트셋에는 생존여부를 나타내는 Survived칼럼이 없다.  
우리는 예측값을 이용해서 이 열을 새로 만들어야 한다.  
그런 다음에, 이 결과를 업로드해서 kaggle을 통해 우리가 예측한 값들을 점수를 매기는데 사용한다.   
   
우선 test데이터셋과 동일한 test_one 변수를 만들자. (test 복사본 만들기.)
  
  
```python
test_one = test
```   
   
   
Survived 칼럼을 0으로 초기화한다.   
   
   
```python   
test_one["Survived"] = 0
```   
   
위에서 우리는 성별과, 나이가 타이타닉 재난의 생존여부에 영향을 끼치는 변수로 가정했는데,
여성이거나 아이(나이가 18미만)이면 "Survived" 칼럼값을 1로 세팅해주자.  
   
   
```python   
test_one["Survived"][test_one["Sex"] == 'female'] = 1
test_one["Survived"][test_one["Age"] < 18] = 1
```   
    
     
- - -   
    
    
Kaggle에서 우리는 트레이닝셋을 통해 만든 모델을 통해 테스트셋의 값을 분류 및 예측해서 제출하고 이를 평가받을 수 있다.  
출력형식이 PassengerId, Survived 칼럼의 내용만 포함되므로 아래와 같이 출력파일을 만들어 케글에 제출해보자.   
    
    
```python
submission = pd.DataFrame({
    "PassengerId" : test["PassengerId"],
    "Survived" : test["Survived"]
})

submission.to_csv("data/submission.csv", index = False)
```   
    
    
지금까지 예측한것을 kaggle에 제출하면 다음과 같은 결과를 확인할 수 있다.  
   
  ![content01](/assets/contents/kaagle_practice_content01.PNG)  
    
    
- - -  

