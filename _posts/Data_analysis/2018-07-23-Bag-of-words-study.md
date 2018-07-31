---
layout: post
title:  "BOW(Bag-Of-Words) 정리"
date:   2018-07-23
author: EunHye Jung
categories: data_analysis
tags:	DataAnalysis DataScience
cover:  "/assets/instacode.png"
---  
  
- - -    
  
*이 글은 아래 참조 사이트를 기반으로 이해한 내용을 개인적인 학습을 목적으로 정리한 것이며, 오역이나 잘못된 내용이 있을 수 있습니다.*
   
- - -    
   
    
## Bag-of-words Model   
   
bag-of-words 모델은 텍스트에서 특징을 추출하는 방법 중 하나로, 머신러닝 알고리즘과 정보검색과 같은 모델링에 이용된다.  
벡터 공간 모델(vector space model)로도 알려져 있다.   
  
즉, 머신러닝 알고리즘에서 텍스트를 사용하려고 하면, 이것을 수치적인 표현(numerical represesntation)으로 변환해야 하며, 이 수치형 표현을 특징 벡터(feature vector)라고 부른다.  
  
bag-of-words 모델은 텍스트에 대하여 특징을 추출하는 방법 중 하나라고 보면 된다.  
bag-of-words 모델은 한 문서의 셋이 입력으로 주어질때, 각 문서에서 각 단어들의 빈도수를 포함하는 테이블을 결과로 출력하는 기계라고 생각하면 된다.    
  
가장 간단한 케이스에서, 단지 하나의 문장로 구성된 문서 셋을 생각해보자   
  
<b> I love dogs </b>  
  
이 문서에 BOW 모델을 적용하면, 다음과 같이 나타낼 수 있다.  
   
   
| <center></center>| <center>I</center> |<center>love</center> |<center> dog </center> |
|--------|--------|--------|--------|
|<center>Doc 1</center>|<center>1</center>|<center>1</center>|<center>1</center>|
    
    
Bag Of Words 모델은 위와 같은 표를 결과물로 내놓게 되는데,  
각 행이 문서에 해당하고, 각 열은 고유한 단어를 나타낸다.  
각 셀들은 문서에서 해당 단어가 나타난 빈도수를 나타내게 된다.   
  
우리는 위의 테이블로부터 어떠한 인사이트(insight)도 얻을 수 없다. 왜냐면 위에 예는 단지 하나의 문서만 고려되었기 때문이다.   
위의 테이블에서 각 열은 문서내에 나타난 고유한 단어를 뜻하게 되는데, 하나의 문서에서 추출된 고유한 단어를 하나의 문서가 모두 포함하고 있을것이기 때문에, 테이블의 각 셀은 1로 채워지게 된다.   
   
Bag Of Words 모델은 (하나가 아닌 여러)문서들의 셋(set)을 비교하기 위해 만들어졌다.    
  
다음과 같이 3개의 문장들로 구성된 문서들의 셋(set)을 생각해보자.  
   
<b> I love dogs </b>  
<b> I hate dogs and knitting </b>  
<b> Knitting is my hobby and my passion </b>   
   
이 문서들에 대해 BoW를 적용해보면 다음과 같은 결과물을 얻을 수 있을 것이다.   
   
   
| <center></center>| <center>I</center> |<center>love</center> |<center> dog </center> |<center> hate </center> |<center> and </center> |<center> knitting </center> |<center> is </center> |<center> my </center> |<center> hobby </center> |<center> passion </center> |
|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------|
|<center>Doc 1</center>|<center>1</center>|<center>1</center>|<center>1</center>|<center></center>|<center></center>|<center></center>|<center></center>|<center></center>|<center></center>|<center></center>|
|<center>Doc 2</center>|<center>1</center>|<center></center>|<center>1</center>|<center>1</center>|<center>1</center>|<center>1</center>|<center></center>|<center></center>|<center></center>|<center></center>|
|<center>Doc 3</center>|<center></center>|<center></center>|<center></center>|<center></center>|<center>1</center>|<center>1</center>|<center>1</center>|<center>2</center>|<center>1</center>|<center>1</center>|           
   
BoW는 문서내의 단어 빈도만 고려한다.  
BoW에서 문서의 중요한 단어들은 문서내에서 가장 많이 나타난 단어들이 된다.  
우리는 위의 테이블에서 단어 love가 첫번째 문서에서만 나옴을 확인할 수 있고,  
단어 hate가 두번째 문장에서만 나타나고,  
단어 hobby와 passion이 세번째 문장에만 나온것을 확인할 수 있다.   
BoW모델을 사용하여 여러 문서에서 중요한 단어가 무엇인지 식별할 수 있다.  
   
   
- - -   
   
### 어휘 관리하기 (Managing Vocabulary)   
  
Bag of Words에서 문장에서 추출되는 단어들의 조합을 어휘(Vocabulary)라고 할 수 있는데,   
이 어휘의 크기가 증가할 수록 문서들의 벡터 표현 크기또한 증가하게 된다.  
예제에서 살펴본것처럼, 문서 벡터의 길이는 알려진(문서내에 나온) 단어들의 개수와 동일하다.  
만약 어휘의 크기가 매우매우 크다면, (수천권의 책에서 어휘를 추출한다고 생각해보자.)  
벡터의 크기 또한 매우 커질 것이다.  
그리고 만약에 각 문서가 어휘에 있는 단어들을 매우 조금씩만 가지고 있다면, 0을 가진 벡터들이 많을것이다. (희소벡터(sparse vector))   
희소 벡터들은 불필요한 메모리와 컴퓨터 자원들을 요구할 것이며, 이것은 자원의 낭비를 초래하게 될것이다.   
  
따라서, bag-of-words 모델을 사용할때 어휘의 크기를 줄이는것이 좋다.  
어휘의 크기를 줄이는 간단한 기술로는 다음과 같은 것이 있따.  
- 대소문자 무시(Ignoring Case)  
- 구두점 무시(Ignoring Punctuation)  
- 불용어라 불리는 특별한 정보를 가지고 있는 않은 단어들을 무시(ex) "a", "of"와 같은)  
- 철자가 잘못된 단어들을 고침 (Fixing misspelled words)  
- 스테밍 알고리즘(stemming algorithm)을 사용해서, 어간을 제거함.   
  ex) "playing", "played"에서 "play" 추출  
  
이런 기본적인 방법들 외에도 어휘를 줄이는 많은 정교한 접근법들이 존재한다.  
    
   
- - -   
     
[참조1](https://en.wikipedia.org/wiki/Bag-of-words_model)   
[참조2](https://machinelearningmastery.com/gentle-introduction-bag-words-model/)   
[참조3](http://datameetsmedia.com/bag-of-words-tf-idf-explained/)    
   
   　
