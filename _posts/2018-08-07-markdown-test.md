---
layout: post
title:  "Markdown-Test"
date:   2018-08-07
author: EunHye Jung
categories: python
comment : true
tags:	
cover:  "/assets/instacode.png"
---   
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
{% raw %}{% highlight html %}
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
{% endraw %}    
  ```   
   
   
- - -

* 작성한 CSS파일을 HTML에 추가하려면 `blog/templates/blog/post_list.html`파일을 다음과 같이 수정.    
    
  <b>blog/template/blog/post_list.html</b>       
   ```html    
{% raw %}{% highlight html %}
   {% load static %} 
   <html>
   <head>
        <title>Django  blog</title>
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
        <link rel="stylesheet" href="{% static 'css/blog.css' %}">
   </head>
   </html>
{% endraw %}    
   ```
   
  
