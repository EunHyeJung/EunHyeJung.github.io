---
layout: post
title:  "Django 설치, 프로젝트, 앱 생성"
date:   2018-08-05
author: EunHye Jung
categories: python
comment : true
tags:	Django 장고 파이썬 Python
cover:  "/assets/instacode.png"
---   
   
   
- - -   
        
####  <font color = "#0E4D92"> 가상환경(Virtual Environmnet) 만들기  </font> 
  
* `virtualenv`를 만드는데 필요한 것은 생성할 곳을 정하면됨.   
   
* 가상환경을 만들 디렉토리로 이동한 다음 다음 명령어를 입력하면 가상환경이 만들어진다.       
  
    <b> command line</b>   
  `$python -m venv myvenv`   
   
    
####<font color = "#0E4D92"> 가상환경 사용하기(Windoows)  </font>
  
   <b> command line</b>   
  `C:\Users\EunHye\dev\djangoproject> myvenv\Scripts\activate`   
   
* 콘솔의 프롬포트 앞에 `(myvenv)` 접두어가 붙어있다면 virtualenv가 시작되었음을 알 수 있음.  
   
   
_ _ _  
   
   
#### <font color = "#0E4D92"> 장고 설치하기(Windoows)    </font>
    
* `pip`가 최신버전인지 확인하기   
  
   <b> command line</b>   
  `(myvenv)~$ python -m pip install --upgrade pip`   
  
  
* 장고 설치하기    

   `django~=` 뒤에 설치하고자 하는 장고 버전을 입력해주면 된다.   
   이때, 파이썬 버전별 지원하는 장고버전을 맞춰주지 않으면 오류가 발생할 수 [여기](https://docs.djangoproject.com/ko/2.0/faq/install/)에서 장고버전과 파이썬버전을 잘 확인해서 설치할것.   
  
   <b> command line</b>   
  `(myvenv)~$ pip install django~=2.0`   
   
   
* 장고 버전 확인하기   
  
   <b> command line</b>   
  `$python -m django --version`   
   
   
_ _ _  
   
   
####  <font color = "#0E4D92"> 장고 프로젝트 생성하기 (Creating a project)  </font>   
  
  
* 장고 프로젝트 생성  
  아래 명령어에서 project_name에는 만들고자 하는 프로젝트의 이름을 넣어주면됨.  
  명령어 마지막 `.`은 현재 디렉토리에 프로젝트를 생성하겠다는 뜻.  
  
  <b> command line</b>   
  `(myvenv) C:\Users\EunHye\dev\djangoproject\> django-admin.py startproject project-name .`   
   
  프로젝트 생성이 완료되면, `django-admin.py`는 스크립트로 디렉토리와 파일을 생성함.  
  스크립트 실행 후 아래와 같은 디렉토리 구조를 확인할 수 있다.   
   
  djangoproject    
  　　├───manage.py   
　　└───projectname  
   　　　　　　 └───settings.py   
   　　　　　　 └───urls.py   
   　　　　　　 └───wsgi.py    
   　　　　　　 └─── __init__.py    
   
  `djangoproject`(루트디렉터리)는 프로젝트를 위한 컨테이너이다.  
  이름을 바꾸고 싶으면 바꿔도 되고, 프로젝트명칭은 장고에게 특별한 문제가 되지 않음.  
  `manaye.py`는 커민드라인 유틸리티이다. 사이트 관리를 도와주는 역할을 하며, 이 스크립트로 다른 설치작업 없이 컴퓨터에서 웹서버를 실행시킬 수 있다.  
  `projectname`에는 실제 프로젝트를 위한 파이썬 패키지들을 담고있다. 
  `projectname/settings.py`는 웹사이트에 관련된 설정정보를 담고 있는 파일이다.  
  `projectname/urls.py`는 장고프로젝트에 사용되는 url들이 모여있는곳. (urlresolver가 사용하는 패턴목록을 담고 있음.)    
   
   
- - -   
     
   
####  <font color = "#0E4D92"> 장고 프로젝트 구동 및 테스트  </font>   
  
      
  <b> command line</b>   
  `(myvenv) ~/projectname$ python manage.py runserver`   
    
  `127.0.0.1:8000`로 접속해서 정상적으로 페이지가 나오는지 확인
   
   
- - -   
     
   
####  <font color = "#0E4D92"> 장고 앱 생성하기   </font>   
  
  
* 장고 프로젝트 환경이 만들어졌다면, 여러개의 앱을 만들어 볼 수 있는 상태가 된것임.  
* 장고에서 만드는 각 애플리케이션은 특정 규칙을 따르는 파이썬 패키지로 구성됨.  
  (장고에서는 하나의 프로젝트가 여러개의 앱을 가진다, 만들어진 앱은 여러 프로젝트에서 재사용이 가능)   
  
* 장고 앱 생성 명령어를 입력하면, 장고는 자동으로 응용 프로그램의 디렉토리 구조를 생성해준다.  
  (이로써 우리가 코드작성에만 집중할 수 있도록 해준다.  ) 
         
  <b> command line</b>   
  `(myvenv) ~$ python manage.py startapp app-name`   
    
* 앱을 생성하고 난 다음 장고에게 이 앱을 사용할것이라고 알려줘야 한다.  
  `projectname/setting.py`에 `INSTALLED_APPS`에 위에서 만든 `app-name`을 추가해준다.   
     
   <b> projectname/setting.py </b>      
  ```python
  INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'app-name',  # 새로 생성한 앱 추가 
]
```    
   
   
- - -   
     
   
####  <font color = "#0E4D92"> 뷰 작성해보기   </font>   
  
    
* 생성한 App이름으로 된 폴더 하위에 `views.py` 파일이 있음.   
* 다음과 같은 코드를 작성해준다.   
  
  <b>appname/vies.py </b>
  ```python
  from django.http import HttpResponse  
  
  def index(request):
  	return HttpResponse("Hi, This is Firat Page")
  ```
  
  
* 위에서 작성한 뷰코드를 호출해주려면, 이 뷰를 URL과 매핑시켜줘야한다.   
  앱 폴더 하위에 <b>urls.py</b> 파일을 생성하고, 다음과 같이 코드를 넣어주자. 
  
  <b>appname/urls.py </b>
  ```python
  from django.urls import path
  from . improt views
  
  urlpatterns = [
   	path(' ', views.index, name='index'), 
  ] 
  ```   
  
  다음 단계는 appname.urls 모듈에서 루트 URLconf를 가리키도록 해야한다.  
  projectname/urls.py에서, django.urls.include를 import 해주고,  
  urlPattern에서 위에 작성한 index url관련한 코드를 아래와 같이 삽입해준다.   
  
  <b>projectname/urls.py </b>
  ```python
  from django.contrib import admin
  from django.urls import include, path
  
  urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('index.urls'))
  ] 
  ```     
  
  <b>include()</b> 함수는 다른 URL 설정들을 참조하도록 해준다.  
  장고가 include() 함수를 마주치게 되면, 해당 부분과 일치하는 URL의 부분을 잘라내고, 남은 문자열 부분을 후속 처리를 위해 include된 URLconf로 전달한다.  
  
  <b>admin.site.urls</b>를 제외한, 다른 URL 패턴을 include 할때마다 항상 include()를 사용해야한다.  
  
* 이제 다시 서버를 기동시켜서 'Hi, This is Firat Page'가 적힌 페이지가 화면에 나타나는지 확인한다.  
      
  <b> command line</b>   
  `(myvenv) ~/projectname$ python manage.py runserver`   
    
   
  
- - -   
   
[참조(장고걸스)](https://tutorial.djangogirls.org/ko/django_installation/)   
[참조(django-docs)](https://docs.djangoproject.com/ko/2.0/intro/tutorial01/)   
  
   
   
   