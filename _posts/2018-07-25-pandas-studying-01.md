---
layout: post
title:  "Pandas(판다스) 이용해서 데이터 색인&필터링"
date:   2018-07-25
author: EunHye Jung
categories: bigdata
tags: bigdata
cover:  "/assets/instacode.png"
---  
   
- - -    
     
*이 글은 [참조 사이트](https://www.kaggle.com/sohier/tutorial-accessing-data-with-pandas)를 기반으로 이해한 내용을 개인적인 학습을 목적으로 정리한 것이며, 오역이나 잘못된 내용이 있을 수 있습니다.*
   
- - -   
   
### Tutorial : Accessing Data with Pandas    
   
이 튜토리얼을 통해 Pandas를 이용해서 데이터를 색인하고 필터링하는 법을 배워본다.  
  
* 판다스 라이브러리 import하고 액셀파일을 불러오기   
  pandas.read_csv의 파라미터값으로는 파일명 외에 여러가지 파라미터값들이 올 수있는데  
  파라미터로 index_col 값을 지정해주면 데이터 프레임 내의 특정한 열을 행인덱스로 지정할 수 있다.  
  
  
  ```python  
  import pandas as pd
  df = pd.read_csv('data/parks.csv', index_col = ['Park Code'])
  df.head(3)
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
      <th>Park Name</th>
      <th>State</th>
      <th>Acres</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
    <tr>
      <th>Park Code</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ACAD</th>
      <td>Acadia National Park</td>
      <td>ME</td>
      <td>47390</td>
      <td>44.35</td>
      <td>-68.21</td>
    </tr>
    <tr>
      <th>ARCH</th>
      <td>Arches National Park</td>
      <td>UT</td>
      <td>76519</td>
      <td>38.68</td>
      <td>-109.57</td>
    </tr>
    <tr>
      <th>BADL</th>
      <td>Badlands National Park</td>
      <td>SD</td>
      <td>242756</td>
      <td>43.75</td>
      <td>-102.50</td>
    </tr>
  </tbody>
</table>
</div>
    
    
_ _ _    
    
    
#### Indexing : Single Rows    
  
* 행(row)에 접근하는 가장 간단한 방법은  `.iloc`메소드의 파라미턱값으로 행번호를 지정하는 것이다.  
  
```python   
df.iloc[2]  

# Park Name    Badlands National Park
# State                            SD
# Acres                        242756
# Latitude                      43.75
# Longitude                    -102.5
# Name: BADL, dtype: object
```
  
  
* 데이터프레임의 색인값을 `.loc`의 파라미터값으로 지정하여서 특정 행에 접근할수도 있다.    
   
```python   
df.loc['BADL']  

# Park Name    Badlands National Park
# State                            SD
# Acres                        242756
# Latitude                      43.75
# Longitude                    -102.5
# Name: BADL, dtype: object
```   
    
    
_ _ _    
    
    
#### Indexing : Multiple Rows    
   
* 여러개의 행을 추출하고자 할경우, 여러개의 인덱스값을 넘겨주면 된다.    
   
```python   
df.loc[['BADL', 'ARCH', 'ACAD']]   
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
      <th>Park Name</th>
      <th>State</th>
      <th>Acres</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
    <tr>
      <th>Park Code</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BADL</th>
      <td>Badlands National Park</td>
      <td>SD</td>
      <td>242756</td>
      <td>43.75</td>
      <td>-102.50</td>
    </tr>
    <tr>
      <th>ARCH</th>
      <td>Arches National Park</td>
      <td>UT</td>
      <td>76519</td>
      <td>38.68</td>
      <td>-109.57</td>
    </tr>
    <tr>
      <th>ACAD</th>
      <td>Acadia National Park</td>
      <td>ME</td>
      <td>47390</td>
      <td>44.35</td>
      <td>-68.21</td>
    </tr>
  </tbody>
</table>
</div>
   
   
* 행을 추출하는 방법 중에 데이터 프레임을 슬라이싱하는 방법도 있다.   
   
```python 
df[:3]
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
      <th>Park Name</th>
      <th>State</th>
      <th>Acres</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
    <tr>
      <th>Park Code</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ACAD</th>
      <td>Acadia National Park</td>
      <td>ME</td>
      <td>47390</td>
      <td>44.35</td>
      <td>-68.21</td>
    </tr>
    <tr>
      <th>ARCH</th>
      <td>Arches National Park</td>
      <td>UT</td>
      <td>76519</td>
      <td>38.68</td>
      <td>-109.57</td>
    </tr>
    <tr>
      <th>BADL</th>
      <td>Badlands National Park</td>
      <td>SD</td>
      <td>242756</td>
      <td>43.75</td>
      <td>-102.50</td>
    </tr>
  </tbody>
</table>
</div>
   
   
```python   
df[3:6]
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
      <th>Park Name</th>
      <th>State</th>
      <th>Acres</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
    <tr>
      <th>Park Code</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BIBE</th>
      <td>Big Bend National Park</td>
      <td>TX</td>
      <td>801163</td>
      <td>29.25</td>
      <td>-103.25</td>
    </tr>
    <tr>
      <th>BISC</th>
      <td>Biscayne National Park</td>
      <td>FL</td>
      <td>172924</td>
      <td>25.65</td>
      <td>-80.08</td>
    </tr>
    <tr>
      <th>BLCA</th>
      <td>Black Canyon of the Gunnison National Park</td>
      <td>CO</td>
      <td>32950</td>
      <td>38.57</td>
      <td>-107.72</td>
    </tr>
  </tbody>
</table>
</div>
   
    
_ _ _    
    
    
#### Indexing : Columns   
   
* 우리는 괄호에 열의 목록을 입력하여, 데이터프레임에 있는 열의 부분집합을 얻을 수 있다. 
   
```python  
df['State'].head(3)   
    
# Park Code
# ACAD    ME
# ARCH    UT
# BADL    SD
# Name: State, dtype: object
```    
  
  
* 또한 `df.State.heads(3)` 이런식으로 칼럼명을 통해 데이터를 추출할 수있지만 이 방법을 이용하려면 열의 이름이 공백이어서는 안되고, 기본문자(character)로 구성된 경우에만 가능하다.  
`df.State.haed()`는 가능한 방법이지만 `df.Park Code`는 불가능하다.  
    
깔끔한(?) 칼럼명을 사용하는 것은 좋은 습관이다. 일반적으로, 칼럼명들은 소문자로 구성되어야 한다. (Pandas는 대소문자 구분을 한다)  
칼럼명을 정제하는 코드는 다음과 같다.   
  
```python  
df.columns = [ col.replace(' ', '_').lower() for col in df.columns ]

print(df.columns)  
# Pandas is case sensitive, so future calls to all of the columns will need to be updated.
```
   
    
_ _ _    
    
    
#### Indexing : Columns and Rows  
  
만역 특정 칼럼과 행의 데이터를 추출하고자 할 경우 다음과 같이 이용할 수 있다.   
   
```python   
$ 'state', 'acres' 칼럼에서 5개의 행 추출
df[['state', 'acres]][:5]
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
      <th>state</th>
      <th>acres</th>
    </tr>
    <tr>
      <th>Park Code</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ACAD</th>
      <td>ME</td>
      <td>47390</td>
    </tr>
    <tr>
      <th>ARCH</th>
      <td>UT</td>
      <td>76519</td>
    </tr>
    <tr>
      <th>BADL</th>
      <td>SD</td>
      <td>242756</td>
    </tr>
    <tr>
      <th>BIBE</th>
      <td>TX</td>
      <td>801163</td>
    </tr>
    <tr>
      <th>BISC</th>
      <td>FL</td>
      <td>172924</td>
    </tr>
  </tbody>
</table>
</div>  
    
