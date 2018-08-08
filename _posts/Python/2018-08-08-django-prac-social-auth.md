---
layout: post
title:  "Django Social Login(Google OAuth2)"
date:   2018-08-08
author: EunHye Jung
categories: python
comment : true
tags:	Django 장고 파이썬 Python
cover:  "/assets/instacode.png"
---   

  
- - -    
   
[참고1](https://medium.com/trabe/oauth-authentication-in-django-with-social-auth-c67a002479c1)  
[참조2](https://hashedin.com/blog/a-guide-to-using-social-login-with-django/)    
[생활코딩(구글API를 통해서 배우는 인증)](https://opentutorials.org/course/2473/16571)   
  
- - -   
　   
   
  
### Social-Auth-App-Django   
   
Social-Auth-App-Django는 오픈소스 파이썬 모듈이다.     
사용자 등록 및 로그인을 소셜 사이트 인증을 통해 제공해준다.   
   
- - -   

#### 필요한 라이브러리 설치
  
장고 프로젝트에서 pip를 통해 social-auth-app-django를 설치.   
  
  
```python
pip install social-auth-app-django
```   
  
    
그리고 나서 `social_django`를 setting.py파일에서 INSTALLED_APP 목록에 추가해주고,
다음 명렁어를 통해 데이터베이스를 migrate 해준다.  
    
<b>settin.py</b>
    
```python
INSTALLED_APPS = [
    ...
    'socal_django'
]

```     
    
    
```python   
python manage.py migrate
```  
  
  
migrate 후에 amdin페이지를 방문하면, SOCAIL_DJANGO 앱이 생성되어있는걸 확인할 수 있다.   
  
  
  ![content01](/assets/contents/django/content01.PNG)      
  
   
     
- - -   
   
   
#### AUTHENTICATION_BACKENDS 설정 추가  
   
  
`setting.py` 파일에 아래와 같이 AUTHENTICATION_BACKENDS 설정을 추가해주자.  
   
<b> setting.py </b>
```python
AUTHENTICATION_BACKENDS = [
    'social_core.backends.google.GoogleOAuth2',
    'django.contrib.auth.backends.ModelBackend',
]
```   
  
  
_ _ _  
   
   
#### Google OAuth2 Credentials 획득   
     
  
* 소셜 로그인을 사용하려면 Google에서는 `Google+API` 활성화하고, `OAuth2.0 클라이언트 ID`를 '웹 애플리케이션'으로 생성해 API Key/Secret을 발급받아야한다.  
  [Google Developer Console](https://console.developers.google.com/apis/dashboard?project=showmethemoney-140006&duration=PT1H) 페이지에서 프로젝트를 생성하고, API Key/Secret을 발급받자.  
(Google Login은 Google+API에 연결되어있다.)    
  
* 발급받은 API Key/Secret 값을 setting.py에 아래와 같이 넣어주자.  
  
  <b> setting.py </b>
```python    
SOCIAL_AUTH_GOOGLE_OAUTH2_KEY = '발급받은 KEY'   
SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET = '발급받은 SECRET'  
```    
  
  
_ _ _  
   
   
#### 로그인, 로그인 후 리다이렉트 시킬 URL 설정
     
  
* 추가적으로 `LOGIN_URL`과 `LOGIN_REDIRECT_URL`, `LOGOUT_REDIRECT_URL` 설정을 해준다.  
  social-app-django는 LOGIN_URL 키를 사용하여, 사용자를 Google 인증 페이지로 리다이렉션한다.  
  LOGIN_REDIRECT_URL과 LOGOUT_REDIRECT_URL 값은 사용자가 로그인하거나 로그아웃할때 설정된 곳으로 리다이렉트된다.  
  
  <b>setting.py</b>  
  ```python  
   LOGIN_URL = '/'
   LOGIN_REDIRECT_URL = '/'        # 로그인 후 redierct 시킬곳
  ```  

  URL 매핑을 위하여 NAME_SPACE도 추가.  
   
  <b>setting.py</b>    
  ```pyhotn
  SOCIAL_AUTH_URL_NAMESPACE = 'social'
  ```

  
* `urls.py` 파일을 열어 소셜 로그인과 로그아웃 url을 추가해준다.   
   참고한 사이트에서는 `from django.contrib.auth.views import logout`를 사용하였는데 django 2.1버전부터는 `from django.contrib.auth import logout`을 사용하는것으로 변경된듯.  
   [참고](https://stackoverflow.com/questions/50669185/python-from-django-contrib-auth-views-import-logout-importerror-cannot-import-n)   
  
  <b>authentication/urls.py</b>  
  	
  ```python   
	from django.urls import path, include
    from . import views
    from django.contrib.auth import logout
  	urlpatterns = [
        path('', include('social_django.urls', namespace='social')),
        path('logout/', views.logout, name='logout')
    ]
  ```  
  
  
_ _ _  
   
   
#### 로그인, 로그아웃 버튼 html 코드    
  
{% raw %} 
```html  
	{% if user.is_authenticated %}
      <p>Logged as {{ user.username }}</p>
      <a class="btn btn-primary" href="{% url 'logout' %}">Logout</a>
    {% else %}
      <a class="btn btn-primary" href="{% url 'social:begin' 'google-oauth2' %}">
        Login
      </a>
    {% endif %}
```
{% endraw %}     
     
    
    
    