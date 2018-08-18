---
layout: post
title:  "Django Debug-Toolbar 이용하기"
date:   2018-08-18
author: EunHye Jung
categories: python
comment : true
tags:	Django 장고 파이썬 Python
cover:  "/assets/instacode.png"
---   
    

* Django 웹프로젝트를 디버깅하기 위해서는 [django-debug-toolbar](https://django-debug-toolbar.readthedocs.io/en/stable/)를 사용할 수 있다.  
이 툴을 사용하면 웹 브라우저에서 해당 웹페이지에서 사용된 HTTP 헤더, Settings, SQL, 템플릿 계층 구조등을 확인할 수 있다.  
    
    
    
#### Django Debug Toolbar 설치   
   
    
1) 가상환경에서 pip를 사용하여 <b>django-debug-toolbar</b> 패키지 설치  
  
`(venv1)~$ pip install django-debug-toolbar`   
   

2) django-debug-toolbar 패키지가 설치되었으면, 웹 프로젝트 세팅 파일(setting.py)의 INSTALLED_APP에 <b>debug_toolbar</b>를 추가해준다.  
  
  
```python  
INSTALLED_APPS = [
    . . .
    'debug_toolbar'
]
```  

  
  
3) MIDDLEWARE 부분에 `debug_toolbar.middleware.DebugToolbarMiddleware`을 추가해준다.  
  
  
```python  
MIDDLEWARE = [
    . . .
    'debug_toolbar.middleware.DebugToolbarMiddleware',
]
```  
  
4) <b>setting.py</b>에 `INTERNAL_IPS ` 지정  
Debug Toolbar는 `INTERAL_IPS`에 세팅되어 있는 IP에서만 확인가능하다.  
  
```python  
INTERNAL_IPS  = [ '127.0.0.1' ]
```  

  
  
5)프로젝트 url 설정파일에 Debug Toolbar URL을 아래와 같이 설정해준다.  
  
```python   
from django.conf import settings
from django.conf.urls import include, url

if settings.DEBUG:
    import debug_toolbar
    urlpatterns = [
        url(r'^__debug__/', include(debug_toolbar.urls)),
    ] + urlpatterns
```
  
  
위의 설정작업을 마치고, 다시 접속해보면 화면 오른쪽에 디버깅 툴바가 나타나는것을 확인할 수 있다.  
  
   
![content01](/assets/contents/django/content02.PNG)  
   
   
   
   







  

