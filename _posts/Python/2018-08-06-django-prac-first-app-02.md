---
layout: post
title:  "Django 블로그 App 만들어보기(STEP-2)"
date:   2018-08-06
author: EunHye Jung
categories: python
comment : true
tags:	Django 장고 파이썬 Python
cover:  "/assets/instacode.png"
---   
    
      
- - -      
   
[참조(장고튜토리얼)](https://docs.djangoproject.com/en/2.0/intro/tutorial02/)   
[참조(장고걸스튜토리얼)](https://tutorial.djangogirls.org/ko/django_start_project/)    
  
- - -    
  
  
###  <font color = "#0E4D92"> Blog App 만들어보기 (STEP-2) </font>    
  
_ _ _   
  
#### <font color="#212930"> 뷰에서 쿼리셋을 얻어와 템플릿에게 전달해주기 </font>    
  
* 뷰(View)는 모델과 템플릿을 연결하는 역할을 함.  
* 이전에 만들었던 `Post`들을 뷰에서 보여주고, 이를 템플릿에 전달하기 위해서는 모델을 가져와야 한다.  
  일반적으류 뷰가 템플릿에서 모델을 선택하도록 만들어야함.   
  
* 쿼리셋(QuerySet)은 전달받은 모델의 객체 목록이다.  
  쿼리셋은 데이터베이스로부터 데이터를 읽고, 필터를 걸거나 정렬할 수 있음.  
  
* 뷰에서 모델로부터 쿼리셋을 얻어오고, 얻어온 쿼리셋을 템플릿으로 전달해주는 코드는 아래와 같이 작성된다.  
   
   <b>blog/views.py </b>
   ```python    
   from django.shortcuts import render  
   from django.utils import timezone
   from .models import Post
   
   def  post_list(request):
        post = Post.objects.filter(created_date__lte = timezone.now()).order_by('create_date') # post는 쿼리셋
        return render(request, 'blog/post_list.html', { 'posts' : posts })
        
   ```  
   
  `render()`함수의 매개변수로 첫번째 인자에는 request 객체를 입력하고, 두번째 인자로는 템플릿명을, 세번째 인자로는 뷰에서 템플릿에 전달할 데이터를 딕셔너리 형태로 입력한다. 세번째 인자값의 경우 필수이 아니라 선택이다.  
  위의 예에서는 'posts'라는 키로 모델에서 전달받은 post 객체들을 전달해주고 있는것이다.  
   
   
- - -
  
#### <font color="#212930"> 장고 템플릿 태그 이용하기 </font>     
  
* 장고의 <b>탬플릿 태그</b>는 파이썬코드를 HTML로 바꿔주어 빠르고 쉽게 동적인 웹 사이트를 만들도록 도와준다.  
* 위에서 글목록이 들어있는 `posts` 변수를 템플릿에게 넘겨주었다.  
  이제 넘겨진 `posts` 변수를 HTML에 나타내주기 위해 다음과 같이 post_list.html 파일을 수정해준다.  
  
  <b>blog/templates/blog/post_list.html</b>   
  ```html      
   <!DOCTYPE html>
   <html>
    <head>
        <title>Django blog</title>
    </head>
    <body>
        <div>
            <h1><a href="">Django  Blog</a></h1>
        </div>

        {% for post in posts %}
            <div>
                <p> published : {{ post.published_date }}</p>
                <h1><a href = ""> {{ post.title }} </a></h1>
                <p> {{ post.text | linebreaksbr }}</p>
            </div>
        {% endfor %}
    </body>
  </html>
  ```    
   
   
- - -
  
  
#### <font color="#212930"> 부트스트랩 적용시켜보기 </font>     
   
* 부트스트랩을 적용시키기 위해 `.html` 파일 내 `<head>`에 아래 링크 삽입.  
  
  <b>blog/templates/blog/post_list.html</b>   
  ```html   
  <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
  <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
  ```   
  
  위의 방법은 프로젝트에 새 파일을 추가하는 것이 아닌, 인터넷에 있는 파일을 연결하는것!  
   
   
- - -
  
  
####  <font color="#212930"> 정적파일 다루기 </font>    
  
  * <b> 정적 파일(static files) </b>은 CSS와 이미지 파일에 해당.    
    이 컨텐츠는 요청 내용에 따라 바뀌는 것이 아니기 때문에 모든 사용자들이 동일한 내용을 볼수 있음.  
   
  * 정적파일 경로를 설정해주기 위해 `setting.py`파일을 열어서 `STATIC_URL` 항목 바로 아래에 `STATIC_ROOT`를 추가해준다.  
    
    <b>projname/setting.py</b>  
    `STATIC_URL = '/static'`     
    `STATIC_ROOT = os.path.join(BASE_DIR, 'static')`     

  * 다음으로, "blog" 앱 안에 `static`이라는 새 폴더를 만든다. 그리고 그 안에 `css`라는 새로운 디렉토리를 만들고 `css`디렉토리 안에 `blog.css`파일을 생성한다.   
    
  projname  
    　└─── blog  
      　 　　　└─── static    
      　　　　　　　　└─── css   
      　　　　　　　　　　　　└─── blog.css
  
  CSS 파일에서는 HTML 파일에 있는 각 요소들에 대한 스타일을 정의할 수 있다.  

* `blog.css`파일을 열어서 새로운 스타일을 정의.  
  
  <b>blog/static/css/blog.css</b>    
  ```css    
  h1 a {
  	color :  #FCA205;
  }
  body {
  	padding-left : 15px;
  }
  ```   
   
  `h1 a `는 CSS 셀렉터(Selector)라고 함.  
   h1 요소안에 a 요소를 넣어 스타일을 적용할 수 있다는 뜻.  
   
* 작성한 CSS파일을 HTML에 추가하려면 `blog/templates/blog/post_list.html`파일 가장 첫줄에 `{% load static %}` 코드를 삽입한다음, <head> </head> 사이에 부트스트랩 CSS 파일 링크 다음에 아래와같이 css 파일을 불러오는 코드를 추가  
    
  <b>blog/template/blog/post_list.html</b>   
   ```html   
   {% load static %}
   
   <html>
    <head>
        <title>Django  blog</title>
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
        <link rel="stylesheet" href="{% static 'css/blog.css' %}">
    </head>
   ```   
   
   
* CSS 설정과 관련된 더 자세한 설명은 [여기](https://tutorial.djangogirls.org/ko/css/)를 참고.  
   
   
- - -
  
  
####  <font color="#212930"> 템플릿 확장하기 </font>   
    
* 장고는 웹사이트 안의 서로 다른 페이지에서 HTML 일부를 동일하게 재사용할 수 있는 템플릿 확장(template extending) 기능을 제공함.  
  템플릿 확장을 이용하면 동일한 정보/레이아웃을 사용할때, 모든 파일마다 같은 내용을 반복해서 입력할 필요가 없어지고, 수정할 부분도 한번만 수정하면 됨!   
  
* 기본 템플릿 `base.html`을 `blog/templates/blog/`에 만들어보자.  
  그 다음 아래의 코드를 base.html에 작성한다.  
   
  <b>blog/template/blog/base.html</b>   
  ```html   
  {% load static %}
  <html>
      <head>
          <title>Django Girls blog</title>
          <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
          <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
          <link href='//fonts.googleapis.com/css?family=Lobster&subset=latin,latin-ext' rel='stylesheet' type='text/css'>
          <link rel="stylesheet" href="{% static 'css/blog.css' %}">
      </head>
      <body>
          <div class="page-header">
              <h1><a href="/">Django Girls Blog</a></h1>
          </div>
          <div class="content container">
              <div class="row">
                  <div class="col-md-8">
                  {% block content %}
                  {% endblock %}
                  </div>
              </div>
          </div>
    </body>
  </html>
  ```    
   
   아래 코드는 ↓     
   
   `{% block content %}`  
   `{% endblock %}　　　`  
      
   `block`을 의미한다. 템플릿 태그 {% blaock %}으로 HTML내에 들어갈 수 있는 공간을 만든것이다.  
  이제 base.html을 확장해 다른 템플릿에도 가져다 쓸 수 있게되었다.  
   
   
* 이제 blog/templates/blog/post_list.html에서 위에서 작성한 템플릿 코드를 확장하도록 아래와 같이 코드를 수정한다.  
  
  <b>blog/templates/blog/post_list.html</b>  
  ```html   
  {% extends 'blog/base.html' %}
  {% block content %}
  	  {% for post in posts %}
      	  <div class = "post">
              <div class = "date">
                 {{ post.created_date }}
              </div>
              <h1> <a href= ""> {{ post.title}} </a></h1>
              <p> {{ post.text|linebreaksbr}} </p>
          </div>
      {% endfor %}
  {% endblock %}
  ```
  
   
- - -    
　  
　  　  
