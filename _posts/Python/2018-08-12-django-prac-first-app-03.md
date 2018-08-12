---
layout: post
title:  "Django 블로그 App 만들어보기(Django Form)"
date:   2018-08-12
author: EunHye Jung
categories: python
comment : true
tags:	Django 장고 파이썬 Python
cover:  "/assets/instacode.png"
---   
    
      
- - -      
   
[참조(장고튜토리얼)](https://docs.djangoproject.com/en/2.0/intro/tutorial02/)   
[참조(장고걸스튜토리얼)](https://tutorial.djangogirls.org/ko/django_start_project/)    
[참조(예제로배우는Python프로그래밍)](http://pythonstudy.xyz/python/article/313-Django-%ED%8F%BC-Form)
  
- - -    
  
  
###  <font color = "#0E4D92"> Blog App 만들어보기 (STEP-3) </font>    
  
_ _ _   
  
#### <font color="#212930"> 장고 폼(Form) </font>    
  
* 장고는 Model 클래스로부터 폼을 자동으로 생성하는 기능을 제공하고 있다.  
  모델 클래스로부터 폼 클래스를 만들기 위해서는,   
    1) django.forms.ModelForm 클래스로부터 파생된 사용자 폼 클래스를 정의한다.  
   2) 사용자 폼 클래스 안에 Meta클래스(Inner클래스)를 정의하고,    
     Meta클래스 안 model 속성에 해당 모델 클래스를 지정함.  
     (즉, 어떤 모델을 기반으로 폼을 작성할 것인지 Meta.model을 지정하는것) 
  
* <b> forms.py </b>라는 파일을 blog 디렉토리 안에 만들어보자.  
  그리고 아래의 코드를 작성해준다.  
  
  <b> blog/forms.py </b>  
  ```python   
  from django import forms
  from .models import Post
  
  class PostForm(forms.ModelForm):
    class Meta:
        model = Post
        fields = ('title', 'text', )
  ```   
  
  PostForm클래스는 ModelForm으로부터 파생된 클래스.   
  fields는 모델 클래스의 필드 중 일부만 폼 클래스에서 사용하고자 할 때 지정하는 옵션.  
  (위와 같은 경우는 'title'과 'text'만 사용자로부터 입력받음)  
  
_ _ _  
  
  
#### <font color="#212930"> 폼과 페이지링크 </font>    
  
* 블로그에 게시글을 추가하는 기능을 위해 page-header라는  div에 +(추가)버튼을 그리는 아래의 코드를 추가.  
  
{% raw %}    
  ```html   
  <a href="{% url 'posts' %}" class="top-menu"><span class="glyphicon glyphicon-plus"></span></a>
  ```  
{% endraw %}   
   
  
* 위의 코드를 작성하면, 화면에 + 버튼이 생긴것을 확인할 수 있음.  
  이제 이 버튼이 클릭하면 글쓰기 요청이 날라가는데, 그 링크가 위에서 post라는것을 알 수 있음.  
  글쓰기 요청을 받는 url을 `blog/urls.py`에 추가.  
  
  <b>blog/urls.py</b>   	
  ```python     
  path('/posts', view.post_new, name = 'post_new')
		
  ```
  
* 위에서 게시글 추가하게되면 `post_new`뷰가 이 요청을 처리하게 된다.  
  `post_new`는 두가지 상황을 처리함.  
  
  1) 처음 페이지에 접속했을때 (새 글을 쓰는 폼이 나와야함)   
  2) 폼에 입력된 데이터를 저장할때    

  위의 두 상황을 처리하는 `blog/views.py`에 작성되는 post_new 함수는 다음과 같음.  

  <b>blow/views.py</b>   
  ```python  
   def post_new(request):
      if request.method == "POST":
      		form = PostForm(request.POST)
             if form.is_valid():
 				post = form.save(commit = False)
                post.author = request.user
                post.created_date = timezone.now()
                post.save()
                return redirect('post_list')
      else:
      	form  PostForm()
     return render(request, 'blog/post_edit.html', {'form' : form})
  ```
  
  
_ _ _  
  
  
#### <font color="#212930"> 폼을 그리는 템플릿 </font>    
   
* `blog/templates/blog` 디렉토리 안에 `post_edit.html` 파일 생성.  

  <b>blog/templates/blog/post_edit.html</b>  
  {% raw %}   
  ```html  
     <form method = "POST" class = "post-from"> {% csrf_token %}
     	{{ form.as_p}}
        <button type = "submit" class="save btn btn-default">Save</button>
     </form>
  ```     
  {% endraw %}    
  
  `CSRF(Cross Site Request Forgeries)`는 웹 해킹 기법의 하나, 장고는 이를 방지하는 기능을 위와 같은 태그의 형태로 제공.  
  장고에서 HTTP POST, PUT, DELETE 할 경우 이 태그를 넣어주어야 함.   
  `{{ form.as_p}}`는 폼의 각 필드를 p태그 안에서 레이블과 텍스트로 배치.    
  폼을 렌더링하는 옵션으로는 form, form.as_p, form.as_table, form.as_ul 등이 있음.  
  (이 옵션들은 각 필드를 어떤 HTML 태그로 Wrapping할것인지 결정)   
  
  
  
  
  
  