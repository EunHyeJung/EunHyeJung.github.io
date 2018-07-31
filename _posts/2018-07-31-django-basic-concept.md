---
layout: post
title:  "Django 기본 개념 이해하기"
date:   2018-07-31
author: EunHye Jung
categories: python
comment : true
tags:	Django 장고 파이썬 Python
cover:  "/assets/instacode.png"
---
  　  
  　  

### 장고(Django) 란?
  
* 파이썬으로 작성된 오픈소스 웹 애플리케이션 프레임워크.   
* 장고는 일반적으로 `MTV(Model-Template-View)` 패턴을 따른다.  
  일반적으로 알려진 MVC 패턴과 유사한 개념을 가지는데, 장고에서는 사용자에게 보여주는 화면을 템플릿(Template)이 담당하고, 애플리케이션의 제어 흐름과 로직을 처리하는것은 뷰(View)가 담당한다.  
  MVC 패턴에서 컨트롤러의 역할을 장고에서는 뷰가 담당하고, MVC 패턴에서 뷰의 역할을 템플릿이 담당하게 되는데, 일반적으로 사용하는 이름을 사용하지 않는 질문에 대한은 [여기](https://docs.djangoproject.com/ko/2.0/faq/general/)를 참조하자.  
  
   
- - -   
  
### 장고의 작동흐름   
  
   
![content01](/assets/contents/django-content01.PNG)    
   
   
* 웹 브라우저에서 어떤 이벤트가 발생한다고 하자.  
(여기서 이벤트는 특정 url을 클릭한다던지, 폼에 데이터를 입력해 보내는 등의 액션을 뜻한다)  
  이벤트가 발생하면 장고 서버로 request(이벤트를 처리해달라는)가 들어오게 된다.  
* 장고 서버로 들어온 이벤트에 대해 URL 디스패처가 URL을 분석해서, 적합한 VIEW로 이 요청을 보낸다.  
* VIEW는 사용자 요청을 받아 데이터 베이스 어디에 접근해서 어떤 데이터를 가공할것인지 MODEL에게 알려준다.  
* MODEL은 DB와 커넥션을 해서 필요한 DB 연산을 처리한다.  
* DB가 다시 모델로 결과값을 보내주면 모델이 이것을 뷰로 전달한다.  
  뷰는 우리에게 보내줄 데이터를 다시 TEMPLATE에게 전달해준다.   
* TEMPLATE는 .js나 .html과 같은 페이지를 만들어서 웹브라우저에게 넘겨준다. 
  
  
  
우리가 장고프로젝트를 생성하게 되면 아래 그림처럼 다양한 파일들이 생성된다.  
  
   
![content02](/assets/contents/django-content02.PNG)    
   
   
   
* 주로 녹색네모들이 우리가 실질적으로 다루는것들이라고 생각하면됨!  
* 미들웨어(Middleware)라는것은 우리가 느낄수는 없지만 장고뒤에서 다양한 처리를 도와준다.  
* WSGI는 웹서버와 장고를 적절하게 결합해주는 역할을 담당한다.  
* urls.py파일은 정규표현식으로 구성되어 있다.    
   
   
- - -   
  
  
### Project와 App   
   
* 하나의 프로젝트가 하나의 웹사이트라고 생각하면된다.  
  프로젝트 안에는 다양한 기능들이 있고, 어떤 의미있는 기능들을 App으로 관리한다.   
   
* 프로젝트를 생성할땐 다음과 같은 명령을 이용한다.  
   
 `$ django-admin startproject sampleproject`   
   
 위의 명령어로 프로젝트를 생성하면 다음과 같은 파일구조가 만들어진다.   
 * `setting.py`는 전체 프로젝트를 관리하느 설정파일이다. 
   
   
![content03](/assets/contents/django-content03.PNG)  
   
    
* app 생성은 다음과 같은 명령어를 이용해 생성한다.  
   
 `$ ./manage.py startapp blog
   
   
![content03](/assets/contents/django-content03.PNG)  
   
  admin 파일은 관리자 권한을 가진 사용자가 볼 수 있는 페이지에 대한 내용을 다룬다.  
  models.py는 DB와 관련된 다양한 역할을 수행하며, view는 db로 가져온 데이터를 적절히 가공하는 역할을 담당한다.    
  migrations는 db관련 폴더.   
    
      
- - -   
  
  
### Setting.py  
   
Setting.py는 프로젝트 환경설정에 대한 내용을 담고있다.  
  
* <b>DEBUG</b>   
  디버그 설정
  개발시에는 true값으로 지정해놓고 실제 서비스 배포시에는 false로 설정  
* <b>INSTALLED_APPS</b>   
  pip로 설치한 앱 또는 본인이 만든 app추가   
* <b>MIDDLEWARE_CLASSES</b>   
  request와 response 사이의 주요 기능 레이어   
  (인증, 보안관련 내용을 다룸)   
* <b>TEMPLATES</b>   
  장고 템플릿 관련 설정, 실제 뷰(html)를 관리  
* <b>DATABASES</b>   
  데이터베이스 엔진의 연결 설정
* <b>STATIC_URL</b>   
  정적파일의 URL(css, javascript, image 등)   
   
   
    
      
- - -   
  
  
### Manage.py   
  
프로젝트 관리를 도와줌, 이 스크립트로 다른 설치작업없이 컴퓨터에서 웹서버 실행 가능.  
  
<b> 주요 명령어 </b>  
* `startapp` : 앱 생성  
* `runserver` : 서버 실행   
* `createsuperuser` : 관리자 생성
* `makemigrations app` : app 모델의 변경사항 체크  
* `migrate` : 변경사항을 DB에 반영  
* `shell` : 쉘을 통해 데이터를 확인  
* `collectstatic` : static 파일을 한곳에 모음.  
   
   
- - -   
   
[참고사이트1](https://www.youtube.com/watch?v=LYmZB5IIwAI)   
[참고사이트2](https://tutorial.djangogirls.org/ko/django_start_project/)   
[참고사이트3](http://pythonstudy.xyz/python/article/304-Django-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8)   
　   
   
　   
   
