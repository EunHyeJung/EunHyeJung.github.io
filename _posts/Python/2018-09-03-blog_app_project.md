---
layout: post
title:  "Django Blog App 만들기"
date:   2018-09-03
author: EunHye Jung
categories: python
comment : true
tags:	Django 장고 파이썬 Python
cover:  "/assets/instacode.png"
---   
   

#### <font color ="#0E4D92"> 테이블 설계  </font>   
   
블로그 앱 - 테이블 설계(Post 모델 클래스)    
    
    
<table>
<th> 필드명 </th>  <th> 타입 </th> <th> 제약 조건 </th> <th> 설명 </th>  
<tr> <td> id </td> <td> Integer </td><td>PK, Auto Increment</td><td>기본 키(Primary Key)</td> </tr>  
<tr> <td> title </td> <td> CharField(50) </td><td></td><td>포스트 제목(Primary Key)</td> </tr>
<tr> <td> slug </td> <td> SlugField(50) </td><td>Unique</td><td>포스트 제목 별칭</td> </tr>
<tr> <td> description </td> <td> CharField(100) </td><td>Blank</td><td>포스트 내용 한줄 설명</td> </tr>
<tr> <td> content </td> <td> TextField </td><td></td><td>포스트 내용 기록 </td> </tr>
<tr> <td> created_date </td> <td> DateTimeField </td><td>auto_now_add</td><td>포스트를 생성한 날짜</td> </tr>
<tr> <td> modify_date </td> <td> DateTimeField </td><td>auto_now</td><td>포스트를 수정한 날짜</td> </tr>
</table>  
    
      
      
   
#### <font color ="#0E4D92"> URL 설계  </font>   
   
   
<table>
<th>URL 패턴</th> <th> 뷰 이름 </th> <th> 템플릿 파일명 </th>  
<tr> <td> /blog/ </td> <td> PostLV(ListView) </td> <td> post_all.html </td> </tr>
<tr> <td> /blog/post </td> <td> PostLV(ListView) </td> <td> post_all.html </td> </tr>
<tr> <td> /blog/post/slug/ </td> <td> PostDV(DetailView) </td> <td> post_detail.html </td> </tr>
<tr> <td> /blog/archive/ </td> <td> PostAV(ArchiveIndexView) </td> <td> post_archive.html </td> </tr>
<tr> <td> /blog/2018 </td> <td> PostYAV(YearArchiveView) </td> <td> post_archive_year.html </td> </tr>
<tr> <td> /blog/2018/sep </td> <td> PostMAV(MonthArchiveView) </td> <td> post_archive_month.html</td> </tr>
<tr> <td> /blog/2018/sep/09 </td> <td> PostDAV(DayArchiveView </td> <td> post_archive_day.html </td> </tr>
<tr> <td> /blog/today </td> <td> PostTAV(TodayArchiveView) </td> <td> post_archive_day.html </td> </tr>
</table>   
  
  
  
- - -  
   
    
### Models.py, Urls.py, Views.py 작성하기  
   
      
   
#### <font color ="#0E4D92">  모델 작성 (Models.py) </font>   
   
   
```python  
class Post(models.Model):
    title = models.CharField('TITLE', max_length = 50)
    # slug 칼럼은 제목의 별칭이라고 할 수 있음, unique 옵션을 추가해 특정 포스트를 검색시 기본키 대신 사용
    # allow_unicode 옵션을 추가하면 한글처리 가능  
    slug = models.SlugField('SLUG', unique = True, allow_unicode=True, help_text='one word for title alias')
    description = models.CharField('DESCRIPTION', max_length= 100, blank= True, help_text= 'simple description text.')
    content = models.TextField('CONTENT')
    # auto_now_add 속성은 객체가 생성될때의 시각을 자동으로 기록되게 함.  
    create_date = models.DateTimeField('Create Date', auto_now_add = True)
    # auto_now 속성은 객체가 데이터베이스에 저장될 때의 시각을 자동으로 기록되게 함.  
    modify_date = models.DateTimeField('Modify Date', auto_now = True)

    # 필드 속성외에 필요한 파라미터가 있으면 Meta 내부 클래스로 정의  
    class Meta:
        verbose_name = 'post'  # 테이블의 단수 별칭 
        verbose_name_plural = 'posts'  # 테이블의 복수 별칭
        # db에 저장되는 테이블의 이름을 'my_post'로 지정 
        # 미지정시 디폴트로 '앱명_모델클래스명(blog_post)'을 테이블명으로 지정
        db_table = 'my_post'  
        # 모델객체의 리스트 출력시 modify_date 칼럼을 기준으로 내림차순 정렬
        ordering = ('-modify_date',) 

	# 객체의 문자열을 객체.title 속성으로 표시되도록 함 
    def __str__(self):
        return self.title

	# 이 메소드가 정의된 객체를 지칭하는 URL을 반환. 
    def get_absolute_url(self):
        return reverse('blog:post_detail', args = (self.slog, ))
        
	# modify_date 칼럼을 기준으로 이전 포스트 반환  
    def get_previous_post(self):
        return self.get_previous_by_modify_date()
         
	# modify_date 칼럼을 기준으로 다음 포스트 반환  
    def get_next_post(self):
        return self.get_next_by_modify_date()
```     
      
      
#### <font color ="#0E4D92">  admin.py에 정의한 모델 등록 </font>   
      
      
<b>blog/admin.py</b>
```python
from django.contrib import admin
from blog.models import  Post


class PostAdmin(admin.ModelAdmin):
	# Post 객체를 보여줄때, title과 modify_date를 화면에 출력하라고 지정.  
    list_display = ('title', 'modify_date')
    # modify_date 칼럼을 사용하는 필터 사이드바를 보여주도록 지정  
    list_filter = ('modify_date',)
    # 검색 박스를 표시하고, 입력된 단어는 title과 content칼럼에서 검색하도록 함
    search_fields = ('title', 'content')
    # slug필드는 title 필드를 사용해 미리 채워지도록 함.  
    prepopulated_fields = { 'slug' : ('title',)}

admin.site.register(Post, PostAdmin)
```
      
   
#### <font color ="#0E4D92">  URLconf 작성 (urls.py) </font>   
   
   
<b>mysite/urls.py</b>
  
```python  
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('bookmark/', include('bookmark.urls'), name='bookmark'),
    path('blog/', include('blog.urls'), name='blog')
]
```  
  
  
<b> blog/urls.py </b>   
  
```python
from django.urls import path
from blog.views import *

app_name = 'blog'

urlpatterns = [
    # Example : /
    path('', PostLV.as_view(), name='index'),
    # Example : /post/
    path('post/', PostLV.as_view(), name='post_list'),
    # Example : /post/slug/
    path('post/<slug:slug>/', PostDV.as_view(), name='post_detail'),
    # Example : /archive/
    path('archive/', PostAV.as_view(), name='post_archive'),

    # Example : /2018/
    path('<int:year>/', PostYAV.as_view(), name='post_year_archive'),
    # Example : /2018/sep/
    path('<int:year>/<int:month>/', PostMAV.as_view, name='post_month_archive'),
    # Example : /2018/sep/10
    path('<int:year>/<int:month>/<int:day>/', PostDAV.as_view, name='post_day_archive'),

    # Example : /today/
    path('today/', PostTAV.as_view, name = 'post_today_archive')
]
```         
      
      
#### <font color ="#0E4D92">  뷰 코딩하기 </font>   
      
      
<b> blog/views.py </b>
```python  
from django.shortcuts import render
from django.views.generic import ListView, DetailView
from django.views.generic.dates import ArchiveIndexView, YearArchiveView, MonthArchiveView
from django.views.generic.dates import DayArchiveView, TodayArchiveView

from blog.models import Post


# ListView
class PostLV(ListView):
    model = Post
    template_name = 'blog/post_all.html'  # 템플릿명을 지정하지 않으면 디폴트 템플릿 파일명은 'blog/post_list.html'이 됨.
    context_object_name = 'posts'
    paginate_by = 2


# DetailView
class PostDV(DetailView):
    model = Post


# ArchiveView
class PostAV(ArchiveIndexView):
    model = Post
    date_field = 'modify_date'


class PostYAV(YearArchiveView):
    model = Post
    date_field = 'modify_date'
    make_object_list = True


class PostMAV(MonthArchiveView):
    model = Post
    date_field = 'modify_date'


class PostDAV(DayArchiveView):
    model = Post
    date_field = 'modify_date'


class PostTAV(TodayArchiveView):
    model = Post
    date_field = 'modify_date'

```  
  
  
* `ArchiveIndexView` 제네릭뷰는 테이블로부터 객체 리스트를 가져와, 날짜 필드를 기준으로 최신 객체를 먼저 출력.  
* `YearArchiveView` 제네릭뷰는 테이블로부터 날짜 필드의 연도를 기준으로 객체 리스트를 가져와, 그 객체들이 속한 월을 리스트로 출력
* `MonthArchiveView` 제네릭뷰는 테이블로부터 날짜 필드의 연월을 기준으로 객체 리스트를 가져와, 그 리스트를 출력
* `DayArchiveView` 제네릭뷰는 테이블로부터 날짜 필드의 연원일을 기준으로 객체 리스트를 가져와 그 리스트를 출력  
* `TodayArchiveView` 제네릭뷰는 테이블로부터 날짜 필드가 오늘인 객체 리스트를 가져와, 그 리스트를 출력함.  
      
      
#### <font color ="#0E4D92">  템플릿 코드 작성하기 </font>   
      
      
<b>blog/templates/blog/post_all.html</b>
{% raw %}
```html
<!DOCTYPE html>
<html>
<head>
    <title> Post List </title>
</head>
<body>
<h1> Blog List </h1>

{% for post in posts %}
<h2><a href='{{ post.get_absolute_url }}'> {{ post.title }} </a></h2>

<p> {{ post.description }} </p>
{% endfor %}

<div>
    <span>
    <!-- page_obj는 장고의 Page객체가 들어있는 컨텍스트 변수, 현재 페이지를 기준으로 이전페이지가 있는지 확인 -->
        {% if page_obj.has_previous %}
            <a href ="?page = {{ page_obj.previous_page_number }}">Previous Page</a>
        {% endif %}

        Page {{ page_obj.number }} of {{ page_obj.paginator.num_pages }}

        {% if page_obj.has_next %}
            <a href = "?page= {{ page_obj.next_page_number }}">Next Page</a>
        {% endif %}
    </span>
</div>

</body>
</html>
```

  
  
* <b>템플릿에서 URL 추출 함수 </b>
  템플릿 파일에서 URL을 추출하는 문법은 2가지 있음.  
  `get_absolute_url()` 메소드를 이용하는 방법과 `{% url %}` 템플릿 태그를 사용하는 방법.  
  `{% url %}` 태그는 직접 태그의 인자로 URL 패턴명을 사용하는 반면, `get_absolute_url()` 메소드에서는 간접적으로 URL 패턴명을 사용.  
  `get_absolute_url()` 메소드는 모델 클래스의 메소드로 정의되어 있어야 사용 가능함. 이 메소드를 정의할때 reverse() 함수를 사용하고, reverse()함수의 인자로 URL 패턴명을 사용하고 있음.   
  아래의 두 문장은 동일한 문장임  
  ```html
  <a href = '{{ post.get_absolute_url }}'> {{ post.title }} </a>   
  <a href = "{% url 'blog_post_detail' post.slug %}"> {{ post.title }} </a>  
  ```
  
  
{% endraw %}   
- - -   
  
    
[전체 프로그램 소스](https://github.com/EunHyeJung/Blog-BookmarkApp/tree/master/blog)     
[참조](https://book.naver.com/bookdb/book_detail.nhn?bid=10801625)   
　　  
　   
　  
