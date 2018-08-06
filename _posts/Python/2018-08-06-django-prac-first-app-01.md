---
layout: post
title:  "Django 블로그 App 만들어보기(STEP-1)"
date:   2018-08-06
author: EunHye Jung
categories: python
comment : true
tags:	Django 장고 파이썬 Python
cover:  "/assets/instacode.png"
---   
    
      
- - -      
   
[참조(장고튜토리얼)](https://docs.djangoproject.com/en/2.0/intro/tutorial02/)   
[참조(장고마이그레이션)](https://docs.djangoproject.com/ko/2.0/topics/migrations/)    
[참조(장고걸스튜토리얼)](https://tutorial.djangogirls.org/ko/django_start_project/)    
  
- - -    
  
  
###  <font color = "#0E4D92"> Migrations </font>   
  
* 장고에서 마이그레이션은 우리가 모델을 변경할때 (필드를 추가하거나 삭제하는 행위 등) 이러한 변경사항들을 데이터베이스에 반영하는 방식이다.  
* makemigrations 이후에는 migration 폴더를 확인하는 습관을 갖는게 좋다.  
  (DB에 무엇이 수정되는지 다시 한번 확인하는 습관)  
* makemigrations app-name 처럼 마이그레이션 하는 앱명칭을 명시하는 것이 좋다.   
  (예상치 못한 마이그레이션 방지)  
* 이미 적용한 마이그레이션 파일은 절대로 지우면 안된다.  
* 프로젝트/앱 생성 후 처음 migrate할때는 앱 이름을 명시하지 않는다.  
  장고 기본앱에, 여러 앱에 걸쳐서 적용할 migrate가 있기 때문.   
   
   
<b> command </b>   
```python
# 마이그레이션 파일 생성
python manage.py makemigrations app-name

# 마이그레이션 적용
payhon manage.py migrate app-name

# 마이그레이션 적용 현황 확인
python manage.py showmigrations app-name

# 지정 마이그레이션 SQL 내역
python maange.py sqlmigrate app-name migration-name
```     
  
  
- - -   
   
   
###  <font color = "#0E4D92"> Django 관리자 </font>   
  
* 장고는 모델에 대한 관리용 인터페이스를 모두 자동으로 생성해준다.  
  
#### <font color="212930"> 관리자 생성하기 </font>   
  
<b> command line</b>   
`(myvenv)~$ python manage.py createsuperuser` 
  
* http://127.0.0.1:8000/admin으로 접속해서 생성한 관리자 계정으로 관리자페이지에 접속.   
  
  
- - -   
   
   
###  <font color = "#0E4D92"> Blog App 만들어보기 (STEP-1) </font>     
    
   
#### <font color="#212930"> app 생성 </font>   
  
* 생성한 프로젝트내부에 별도의 블로그 앱을 생성.  
  
  <b> command line</b>   
`(myvenv)~$ python manage.py startapp blog` 
    
* manage.py 파일에  INSTALLED_APP 부분에 'blog'를 추가한다.  
  
   ```python
   INSTALLED_APPS = [
      ...
      'blog',
   ]
   ```   
   
_ _ _    
   
#### <font color="#212930"> 블로그 글 모델 만들기 </font>   
   
* `blog/models.py` 파일에 다음과 같은 코드 작성하여 모델 정의.  
  
   ```python
   from django.db improt models
   form django.utils import timezone
   
   class Post(models.Model):
       author = models.ForeignKey('auth.User, on_delete = models.CASCADE)
       title = models.CharField(max_length = 200)
       text = model.TextField()
       created_date = models.DataTimeField(default = timezone.now)
       
       def __str__(self):
       		return self.title
   
   ```   
   
  * `models.CharField` : 글자수가 제한된 텍스트를 정의할 때 사용  
  * `models.TextField` : 글자수에 제한이 없는 긴 텍스트를 위한 속성  
  * `models.DateTimeField` : 날짜와 시간을 의미  
  * `models.ForeignKey` : 다른 모델에 대한 링크    
   
   
_ _ _    
   
   
#### <font color="#212930"> 데이터베이스에 모델을 위한 테이블 만들기 </font>   
  
   
* 마이그레이션 파일 생성   
  
  <b> command line</b>   
  `(myvenv)~/proj$ python manage.py makemigrations blog`  
  
  생성된 마이그레이션 파일을 열어보면 다음의 내용을 확인할 수 있다.  
    
   <b>blog/migrations/0001_initial.py</b>   
  ```python  
    from django.conf import settings
    from django.db import migrations, models
    import django.db.models.deletion
    import django.utils.timezone

    class Migration(migrations.Migration):
    	initial = True

        dependencies = [
            migrations.swappable_dependency(settings.AUTH_USER_MODEL),
        ]

        operations = [
            migrations.CreateModel(
                name='Post',
                fields=[
                    ('id', models.AutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                    ('title', models.CharField(max_length=200)),
                    ('text', models.TextField()),
                    ('created_date', models.DateTimeField(default=django.utils.timezone.now)),
                    ('author', models.ForeignKey(on_delete=django.db.models.deletion.CASCADE, to=settings.AUTH_USER_MODEL)),
                ],
            ),
        ]
  ```   
  
  
* 마이그레이션 적용    
  실제 데이터베이스에 모델 추가를 반영
  
  <b> command line</b>   
  `(myvenv)~/proj$ python manage.py migrate blog`  
    
    
_ _ _    
   
   
#### <font color="#212930"> 장고 관리자에서 모델 관리해보기 </font>   
  
* 우리가 모델링한 모델들을 관리자페이지에서 추가,수정,삭제 할 수 있다.   
  `blog/admin.py` 파일에 다음과 같이 코드를 수정한다.  
   
   <b>blog/admin.py</b>   
   ```python  
   from django.contrib import admin
   from .models import Post
   
   admin.site.register(Post) # 생성한 모델을 등록  
   ```   
   
* 관리자 페이지 `http://127.0.0.1:8000/admin/`에 다시 접속해보면 위에서 생성했던 BLOG앱의 Post모델에 대한 정보를 관리자 페이지에서 확인할 수 있다.   
   
  
- - -    
   
   
#### <font color="#212930"> 장고 뷰 생성하기 </font>   
  
  * 뷰(View)는 애플리케이션의 로직을 넣는 부분  
  * 뷰는 `모델`에서 필요한 정보를 받아와서, `템플릿`에 전달하는 역할을 담당.   
  
  * post_list라는 함수를 만들어 요청(request)을 받아, blog/post_list.html 템플릿을 보여주도록 함수를 작성하는 코드는 아래와 같다.  
   
   <b>blog/views.py</b>   
   ```python  
   from django.shortcuts import render
   
   def post_list(request):
   		return render(request, 'blog/post_list.html', {})
   ```   
  
  
  
- - -    
   
   
#### <font color="#212930"> 블로그 글 목록을 나타내는 URL 설정하기 </font>   
  
  * `blog` 애플리케이션에서 메인 projectname/urls.py 파일로 url들을 가져온다.  
  
   <b>project-name/url.py</b>   
   ```python  
   from django.contrib import admin
   from django.urls import path
   from django.conf.urls import include
   
   urlpatterns = [
   	path('admin/', admin.site.urls),
        path('', include('blog.urls'))
   ]
   ```   
   
   이제 http://127.0.0.1:8000/로 들어오는 모든 접속 요청을 `blog.urls`로 전송해 추가 명령을 찾을 수 있음.  
  
* `blog/urls.py`이라는 새 파일을 생성해서 아래와 같이 코드를 작성한다.  
  
   <b>blog/url.py</b>   
   ```python  
   from django.urls import path
   from . import  views
   
   urlpatterns = [
      path('', views.post_list, name = 'post_list'),  
   ]
   ```   
   
   path('', views.post_list, name = 'post_list')는 'http://127.0.0.1:8000/`로 접속되면, `views.post_list`를 호출한다.   
   
   
- - -    
   
   
#### <font color="#212930"> 템플릿, HTML 파일 생성하기 </font>   
   
* 템플릿이란 서로 다른 정보를 일정한 형태로 표시하기 위해 재사용 가능한 파일을 말함.  
  예를 들면, 회사의 회의록을 생각해보자.   
  (회의록의 내용은 회의마다 달라질 수 있지만, 모두 동일한 회의록 양식을 사용한다.)   
*  장고 템플릿 양식은 HTML을 사용함.  
  
* 템플릿 생성을 위해 `blog` 디렉토리 안에 하위 디렉토리인 `templates`을 생성하자.  
  그리고 `templates`디렉토리 내에 다시 앱과 동일한 `blog`라는 디렉토리를 생성하자.  
   
   blog   
     　└───templates   
 　   └───blog    
     
  그런 다음, `blog/templates/blog` 디렉토리 하위에 `post_list.html` 파일을 생성해보자.  
  그리고 아래와 같이 간단한 html 테스트코드를 작성.   
   
  <b>blog/templates/blog/post_list.html</b>  
  ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
    <h1>Test Page</h1>
    </body>
    </html>
  ```
  
  이제 다시 서버를 기동시켜서 `http://127.0.0.1:8000`에 접속해보면 'Test Page' 텍스트가 적힌 페이지가 웹화면에 나타나는것을 확인해볼 수 있다.  
   
- - -   
     
     
     
　　  
    　　  
