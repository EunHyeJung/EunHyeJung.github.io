---
layout: post
title:  "지도학습, 비지도학습, 강화학습 개념"
date:   2018-08-15
author: EunHye Jung
categories: data_analysis
tags: bigdata
cover:  "/assets/instacode.png"
---  
    
    
###  <font color = "#0E4D92">   Surpervised Learning </font>     
  
  
* 정답이 있는(labled) 데이터를 주고 이를 컴퓨터가 학습하도록 하는 방법.  
* 보통 예측문제나 회귀문제를 해결하기 위해 많이 사용하며, 학습모델은 규칙 모델, 트리모델, 신경망 모델을 많이 사용.  
* 지도학습은 훈련 데이터를 통해 학습을 하며 모델 함수의 성능을 높임. 
* 예로 Cat이라는 레이블이 달려있는 고양이 사진과와 Dog라는 레이블이 달려있는 강아지의 이미지를 주고 학습하는것.  
   
   
#### Supervised Learning 일반적인 문제  
* 이미지 레이블링 : 태그된(tagged) 이미지로부터 학습  
* 이메일 스팸 필터 : 레이블된 스팸메일과 의미있는 메일들로부터 학습  
* 시험 성적 예측 : 이전 시험성적과 투자한 시간으로부터 학습  
   공부한 시간대비 시험의 성적을 예측하는것 : `regression`   
   공부한 시간대비 시험을 패스/논패스로 나눠 예측 : `binary classification`   
   공부한 시간대비 시험 성적 등급 (A, B, C, E, F)예측 : `multi-label classification`  
   
   
- - -  
    
###  <font color = "#0E4D92">   Unsurpervised Learning </font>     
  
  
* 비지도학습은 정답이 없는(unlabeled) 데이터를 사용.  
* 정답이 없는 데이터에 대해 데이터의 분포를 추정하거나 비슷한 특성을 가진 데이터까리 군(Group)으로 군집화(Clusering)한다.  
* 군집화, 밀도 추정, 차원 축소, 이상치 탐지 등의 알고리즘들이 비지도학습으로 분류될 수 있다.  
   
   
- - -  
    
###  <font color = "#0E4D92">  강화학습 </font>     
  
  
* 행동심리학에서 영감을 받았으며, 어떤 환경 안에서 정의된 에이전트가 현재 상태를 인식하여 선택 가능한 행동들 중 보상을 최대화하는 행등올 선택하는 방법.  
* 에이전트가 어떤 행동을 함으로써 어떤 상태에 도닳하고, 환경은 그 상태에 대한 보상을 제공하며 에이전트는 보상을 통해서 좋은 좋은 행동 정책을 학습해나감.  