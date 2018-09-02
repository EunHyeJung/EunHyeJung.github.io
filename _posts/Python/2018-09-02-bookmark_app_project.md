---
layout: post
title:  "Django Bookmark App 만들기"
date:   2018-09-02
author: EunHye Jung
categories: python
comment : true
tags:	Django 장고 파이썬 Python
cover:  "/assets/instacode.png"
---   
   
   
   
#### 프로젝트 설정 파일 변경   
    
    
* <b>데이터베이스 설정항목 확인</b>  
장고는 디폴트로 SQLite3 데이터베이스 엔진을 사용하도록 설정되어있음.  
(MySQL이나 Oracle, ProgreSQL 등 다른 데이터베이스로 변경 가능)   
  
    
* <b>정적파일 설정</b>  
`STATIC_URL` 항목은 최초 stteings.py 파일이 만들어질때 장고가 해준 그대로.  
`STATICFILES_DIRS` 항목은 프로젝트 정적 파일이 위치한 디렉터리를 의미, 수동으로 직접 지정.  
  
  정적 파일을 찾을 때 각 애플리케이션의 static/ 디렉터리보다 STATICFILES_DIRS 항목으로 지정한 디렉터리를 먼저 검색.    
   
  ```python   
  STATIC_URL = '/static/'
  STATICFILE_DIRS = os.path.join(BASE_DIR, 'static') # 추가  
  ```   
    
   
* <b>타임존 지정</b>  
  한국시간으로 시간설정 변경  
  
  ```python  
   #TIME_ZONE = 'UTC'
  TIME_ZONE = 'Asia/Seoul'
  ```   
    
  
* <b>애플리케이션 등록</b>  
  프로젝트에 포함되는 애플리케이션은 모두 설정 파일에 지정되어야함.  
  애플리케이션을 등록할때는 간단하게 애플리케이션의 모듈명만 등록해도 되지만(ex) 'bookmark')  
  애플리케이션의 설정 클래스로 등록하는것이 더 정확한 방법임.  
   
  ```python  
   INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'bookmark.apps.BookmarkConfig',   # 추가  
   ]
  ```  
   
  `애플리케이션 설정 클래스`는 해당 애플리케이션에 대한 메타 정보를 저장하기 위한 클래스로,  
   django.apps.AppConfig 클래스를 상속받아 작성.   
  앱 설정 클래스는 앱 이름(name), 레이블(label), 별칭(verbose_name), 경로(path) 등을 설정할 수 있으며,  
  이 중 이름(name)은 필수 속성임.  
  만일 INSTALLED_APPS 항목에 애플리케이션을 등록시 설정 클래스 대신에 애플리케이션 디렉터리만 지정하면, __init__.py파일에서 default_app_config 항목으로 지정된 클래스를 설정 클래스로 사용.  
  default_app_config 항목도 지정되어 있지 않으면 장고의 기본 AppConfig 클래스를 설정 클래스로 사용.  
   
   
- - -   
    
    
### 애플리케이션 설계  
  
#### <font color ="#0E4D92"> 화면 UI 설계  </font>   
   
    
#### <font color ="#0E4D92"> 테이블 설계  </font>   
   
북마크 앱 - 테이블 설계(Bookmark 모델 클래스)    
    
<table>
<th> 필드명 </th>  <th> 타입 </th> <th> 제약 조건 </th> <th> 설명 </th>  
<tr> <td> id </td> <td> Integer </td><td>PK, Auto Increment</td><td>기본 키(Primary Key)</td> </tr>  
<tr> <td> title </td> <td> CharField(100) </td><td>Blank, Null</td><td>북마크 제목(Primary Key)</td> </tr>
<tr> <td> url </td> <td> URLField </td><td>Unique</td><td>북마크 URL</td> </tr>
</table>  
    
    
#### <font color ="#0E4D92"> 로직 설계  </font>      
    
로직 설계는 처리 흐름을 설계.   
웹 프로그래밍에서 URl을 받아서 최종 HTML 템플릿 파일을 만드는 과정이 하나의 로직이됨.  
그 과정에서 리다이렉션이 일어날 수 있고, 템플릿 파일에서 URL 요청이 발생할 수도 있음.  
-> 이런 과정들을 모두 고려해서 문서로 표현하는것이 로직 설계 과정!   
  
/bookmark/ 　　->　　`BookmarkLV.as_view()`　　->　bookmark_list.html   
/bookmark/pk 　->　　`BookmarkDV.as_vew()`　　->　bookmark_detail.html        
   
#### <font color ="#0E4D92"> URL 설계  </font>   
  
<b>URL 패턴 </b>  - <b> 뷰 이름 </b> - <b> 템플릿 파일 이름 </b>  
/bookmark/  - BookmarkLV (ListView) - bookmark_list.html  
/bookarmk/pk  - BookmarkDV (DetailView) - bookmark_detail.html  
   
   
- - -   
    
    
### 개발 코딩하기 - 모델  
  
  
#### <font color ="#0E4D92"> 테이블 정의  </font>   
  
테이블은 <b>models.py</b>에 정의.  
장고에서는 테이블을 하나의 클래스로 정의하고,  
테이블의 칼럼은 클래스의 변수(속성)로 매핑함.  
테이블 클래스는 django.db.models.Model 클래스를 상속받아 정의하고,  
각 클래스 변수의 타입도 장고에서 미리 정의해둔 필드 클래스를 사용함.  
  
  
<b>bookmark/models.py</b>  
```python  
from django.db import models  
  
class Bookmark(models.Model):
	title = models.CharField(max_length = 100, blank = True, null = True)
    url = models.URLField('url', unique = True)
    
    def __str__(self):
    	return self.title
```  
  
  
#### <font color ="#0E4D92"> Admin 사이트에 테이블 반영  </font>   
  
  
<b>bookmark/admin.py</b>
```python
from django.contrib import admin
from bookmark.models import Bookmark

class BookmarkAdmin(admin.ModelAdmin):
    list_display =  ('title', 'url')

admin.site.register(Bookmark, BookmarkAdmin)
```   
  
`BookmarkAdmin` 클래스는 Bookmark 클래스가 Admin 사이트에서 어떤 모습으로 보여줄지 정의.  
-> Bookmark 내용을 보여줄 때, title과 url을 화면에 출력하라고 지정함.  
  
`admin.site.register()` 함수를 사용해 Bookmark와 BookmarkAdmin 클래스를 등록함.  
  
★ 테이블을 새로 만들때는 <b>models.py</b>와 <b>admin.py</b> 두 개의 파일을 함께 수정할 것!    
  
  
#### <font color ="#0E4D92"> 데이터베이스 변경사항 반영  </font>   
   
   
`$ python manage.py makemigrations`  
`$ python manage.py migrate`
   
마이그레이션 정보는 애플리케이션 디렉터리별로 존재함.  
  
   
- - -   
    
    
### 개발 코딩하기 - URLconf  
  
  
<b>mysite/urls.py</b>
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('bookmark.urls'))
]
```   
  
  
<b>bookmark/urls.py</b>
```python
from django.urls import path, include
from bookmark.views import BookmarkLV, BookmarkDV

urlpatterns = [
    path('bookmark/', BookmarkLV.as_view(), name = 'index'),
    path('bookmark/<int:pk>', BookmarkDV.as_view(), name = 'detail'),
]
``` 
   
    
- - -
    
    
### 개발 코딩하기 - 뷰    
  
  
앞에서 URLconf를 작성하며 뷰를 클래스형 뷰로 정의하기 위해 각 URL에 따른 해당 클래스 및 as_view() 메소드를 지정하였음.  
URLConf에서 지정한 클래스형 뷰를 작성함.  
  
클래스형 뷰를 작성할 때 가장 먼저 고려할 사항은 <b>어떤 제네릭 뷰를 사용할 것</b>인가 이다. 
개발하고자 하는 애플리케이션의 로직을 분석하여 가장 적합한 제네릭 뷰를 사용한다.  
  
북마크 앱에서는 `ListView`와 `DetailView` 제네릭뷰를 선택해서 사용한다.  
  
  
<b>bookmark/view.py</b>  
```python
# 클래스형 제렉뷰를 사용하기 위해 ListView, DetailView를 import
from django.views.generic import ListView, DetailView 
# 테이블 조회를 위한 모델 클래스 import
from bookmark.models import Bookmark

# ListView
class BookmarkLV(ListView) :
	model = Bookmark 
    
# Detail View
class BookmarkDV(DetailView) :
	model = Bookmark
```  
  
  
* `BookmarkLV`는 Bookmark 테이블의 리스트를 보여주기 위한 뷰 (ListView 제네릭뷰 상속)   
   명시적으로 지정하지 않아도 장고에서 디폴트로 2가지 속성을 알아서 정해줌.   
   1) 컨텍스트 변수로 <b>object_list</b> 사용  
   2) 템플릿 파일을 <b>모델명소문자_list.html</b> 형식의 이름으로 지정 -> 템플릿 파일명은 'bookmark_list.html'이 됨.  
  
* `BookmarkDV`는 Bookmark 테이블의 상세 정보를 보여주기 위한 뷰 (DetailView 제네릭뷰 상속)   
   명시적으로 지정하지 않아도 장고에서 디폴트로 2가지 속성을 알아서 정해줌.  
   1) 컨텍스트 변수로 <b>object</b> 변수를 사용   
   2) 템플릿 파일을 <b>모델명소문자_detail.html</b> 형식의 이름으로 지정 -> 템플릿 파일명은 'bookmark_detail.html'이 됨.    
      
    
- - -
    
    
### 개발 코딩하기 - 템플릿    
  
  
#### <font color ="#0E4D92"> bookmark_list.html 템플릿 작성하기  </font>   
  
<b>bookmark/templates/bookmark/bookmark_list.html</b>   
{% raw %}  
```html
<!DOCTYPE html>
<html>
<head>
    <title> Bookmark List </title>
</head>
<body>
<div id = "content">
    <h1> Bookmark List </h1>
    <ul>
        {% for bookmark in object_list %}
            <li><a href="{% url 'detail' bookmark.id %}"> {{ bookmark }}</a> </li>
        {% endfor %}
    </ul>
</div>
</body>
</html>
```  
{% endraw %}   
  
  
#### <font color ="#0E4D92"> bookmark_detail.html 템플릿 작성하기  </font>   
  
<b>bookmark/templates/bookmark/bookmark_detail.html</b>   
{% raw %}  
```html
<!DOCTYPE html>
<html>
<head>
    <title> Bookmark Detail</title>
</head>
<body>
<div id ="content">
    <h1> {{ object.title }} </h1>
    <ul>
        <li> URL : <a href="{{ object.url }}"> {{ object.url }}</a></li>
    </ul>
</div>
</body>
</html>
```
{% endraw %}   
   
    
- - -   
   
   
### Bookmark App 완성화면   
    
   [전체 프로그램 소스](https://github.com/EunHyeJung/BookmarkApp)    
   
  ![content01](/assets/contents/django/content03.PNG)  
   
   
   ![content01](/assets/contents/django/content04.PNG)  
   
   
- - -  
  
  
[참조](https://book.naver.com/bookdb/book_detail.nhn?bid=10801625)
　　  
    　　  
  
