---
layout: post
title:  "Django 기본 개념 이해하기(모델,URL,뷰)"
date:   2018-08-04
author: EunHye Jung
categories: python
comment : true
tags:	Django 장고 파이썬 Python
cover:  "/assets/instacode.png"
---   
   
   
- - -    
     
*이 글은 [참조 사이트](https://docs.djangoproject.com/en/2.1/intro/overview/)를 기반으로 이해한 내용을 개인적인 학습을 목적으로 정리한 것이며, 오역이나 잘못된 내용이 있을 수 있습니다.*
   
- - -  
   
   
### 모델 설계 (Design your model)   
    
    
* ORM은 객체로 데이터베이스에 접근하는 방식
* Django에서는 모델(models.py)에 만든 클래스(Class)를 통해 객체(Object or Insance)를 만들고, 이 객체를 통해 DB에 접근하게 된다.  
* 예를 들어 USER라는 테이블에서 id값이 1인 username값을 가져오고 싶다고 할때  
   SQL : Select username from USER where id = 1;     
   ORM : User.ojbects.get(id=1).username  

* <b> ModelManager </b>    
  특정 모델에 있는 모든 데이터를 조회할때 `클래스.objects.all()`을 사용한다.  
  여기서 클래스뒤에 붙는 `objects`가 장고에서의 모델매니저(Model Manager)라고 한다.  
  장고의 모델 매니저는 데이터베이스와 장고 모델 사이에서 질의 연산(Query Operations)이 일어나는 인터페이스 역할을 해준다.  
  
* 모델코드 작성 예시   
   
```python   
  from django.db import models.  
  
  class Reoporter(models.Model):
  	full_name = models.CharField(max_length = 70)
    
    def __str__(self):
    	return self.full_name
      
   class Article(models.Model):
   		pub_date = models.DataField()
        headline = models.CharField(max_length = 200)
        content = models.TextField()
        reporter = models.ForeignKey(Reporter, on_delete=models.CASCADE)
        
        def __str__(self):
        	return self.headline
```   
  
  
  2.0버전부터는 related를 구현할때, 필수인자로 `on_delete`값이 추가되었음.  
  `on_delete`를 지정하지 않으면 에러가 발생함.  
   
* 데이터베이스 테이블을 자동으로 생성하기 위해서, 장고 커맨드라인에서 database migrate 명령을 실행해준다.  
   
   `$ python manage.py migrate`   
    
   <b>migrate</b> 명령은 모델코드를 탐색해서 만약에 만들어지지 않은 테이블이 있다면, DB에 테이블을 생성해주는 역할을 담당한다. 
   
   
- - -   
   
  
### URL 설계 (Desgin your URLS)   
   
   
Django 2.0버전부터는 `path()`함수를 사용, 이전에는 `url()`을 사용하여 정규표현식으로 url mapping을 하였음.  
  
  
* urls.py 작성 예시
  
```python   
from django.urls import path  
from . import views  

urlpatterns = [
	path('articles/<int:year>/', views.year_archive),
    path('articles/<int:year>/<int:month>/', views.month_artchive),
    path('articles/<int:year>/<int:month>/<int:pk>/', views.article_detail),
]
```  
  
  
  위 코드는 URL 경로들을 파이썬 콜백 함수("views")로 매핑시켜준다.   
  사용자가 특정 페이지를 요청하면 장고는 urlpattern에서 사용자가 요청한 URL과 일치하는것이 있는지 찾는다. (만약 일치하는것이 없다면, 404에러가 발생함.)  
  이 작업은 path들은 로딩시에 정규표현식으로 컴파일 되기 대문에 매우 빠르게 진행된다.  
   
  만약, URL 패턴이 일치되는것을 찾게되면, 장고는 해당하는 view를 호출한다.  
  각각의 뷰는 요청 메타데이터를 포함하는 요청객체를 전달받게 된다.  
  예를 들어, 만약 사용자가 "article/2005/05/39323/" URL을 요청했다면, 장고는 news.views.article_detail(request, year = 2005, month = 5, pk = 39323) 함수를 호출하게 되는것이다.   
  
   
- - -   
   
    
### 뷰 작성하기 (Writing your views)   
   
  
* Django View는 다음 두가지 중 하나의 역할을 담당한다.  
  1. 요청된 페이지에 대한 내용을 담고 있는 <b>HttpResponse</b> 객체를 반환.   
  2. Http404와 같은 예외를 발생시킴    
   
* 일반적으로, 뷰는 입력 파라미터에 따라 데이터를 찾아서, 템플릿(template)를 로드한 다음 반환되는 데이터와 함께 템플릿을 그린다.   
  
  
* views.py 작성 예시
  
  
```python   
from django.shortcuts import render 

from .models import Article   

def year_archive(request, year):
	a_list = Article.objects.filter(pub_data__year = year)
    context = { 'year' : year, 'article_list' : a_list}
    return render(request, 'news/year_archieve.html', context)
```   
   
     
  
- - -  
  　
  　
[참조](https://docs.djangoproject.com/en/2.1/intro/overview/)  
[참조](https://www.slideshare.net/DustinJunginSeoul/qna-blog-using-django-orm?qid=9a4b0316-dca4-4e8c-99d8-5d6e8f7e466e&v=&b=&from_search=1)   
　  
 　 
