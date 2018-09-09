---
layout: post
title:  "장고 가상 환경 (Django Virtualenv)"
date:   2018-09-09
author: EunHye Jung
categories: python
comment : true
tags:	Django 장고 파이썬 Python
cover:  "/assets/instacode.png"
---  
  
### Django Virtualenv     
  
  　
* 파이썬에서는 프로젝트별로 독립된 가상 환경을 만들어주는 `virtualenv` 툴을 제공.  
  독립된 가상 환경이 필요한 이유는 인터넷에서 다운로드한 파이썬 라이브러리들이 충돌을 일으키는것을 방지하기 위함!   
  (외부 라이브러리들은 서로 의존성을 가지고 있는 경우가 많아 버전이 맞지 않은 경우 오작동을 일으킬 수 있음)   
  
* 외부 라이브러리들을 시스템의 파이썬 라이브러리 디렉터리에 다운로드하는것이 아니라,  
  별도의 개발 환경에 설치함으로써 다른 파이썬 프로그램에는 영향을 주지 않도록 함     
     　
  　
#### 가상환경 만들기  
   
     
virtualenv를 만들때 필요한것은 만들곳을 지정해주기만 하면됨.   
  
    
`$python -m venv virtualenvName`  
    
      
#### 가상환경 사용하기    
   
     
위의 명령어를 통해 가상환경을 만들면 `virtualenvName`라는 이름의 폴더(디렉터리)가 만들어진다.  
(이 폴더안에 우리가 사용할 가상환경이 들어있다.)  
아래 명령어를 통해 가상환경을 실행할 수 있음!  
   
   　
`$ virtualenvName\Scripts\activate`     
  
      
   
    
