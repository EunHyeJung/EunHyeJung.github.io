---
layout: post
title:  "Django Authentication"
date:   2018-09-10
author: EunHye Jung
categories: python
comment : true
tags:	Django 장고 파이썬 Python
cover:  "/assets/instacode.png"
---  
  
  
## <font color = "#8E1600"> Django Authentication   </font>   

* 인증기능은 웹애플리케이션의 필수 기능, 장고가 기본적으로 제공하는 기능 중의 하나.  
  장고 패키지에 포함되어 있는 `django.contrib.auth` 앱이 인증기능을 담당.   
* 장고에서는 User 테이블을 기본으로 제공하고 있음.  
  장고 인증을 담당하는 Auth 앱은 User 테이블 이외에도 Group, Permission 등의 테이블을 정의하고 있음.   
   
- - -   
   
   
### User 테이블 구조 (Django 기본 제공)   
   
   
| 필드명 | 타입 | 제약조건, 디폴트 | 설명 |  
| :---: | :---: | :---: | :---:|  
| id | Integer | PK, Auto Increment | 기본키 |  
| password | CharField(128) | | 비밀번호 |  
|username | CharField(30) | Unique | 로그인 이름 |  
| first_name | CharField(30) | Blank | 사용자 이름 |  
| last_name | CharField(30) | Blank | 사용자 성 |  
| email | CharField(254) | Blank | 이메일 주소 |  
| is_superuser | BooleanField | False | 슈퍼유저(관리자) 여부 |  
| is_staff | BooleanField | False | 스태프 여부 | 
| is_active | BooleanField | True | 계정 활성화 여부 |  
| date_joined | DateTimeField | timezone.now | 계정 생성 시간 |  
| last_login | DateTimeField | Blank, Null | 마지막 로그인 시간 |   

   
  
- - -  
  
  
### 인증 URL (Django 기본 제공)  
  
  
* 장고의 인증기능을 보면, URL과 뷰는 이미 개발되어 있고, 템플릿은 템플릿 파일명만 정해져 있으므로, 그 템플릿 내용을 직접 채워넣어줘야 한다.  
(장고에서 기본적으로 제공되는것들이지만, 모두 커스터마이징이 가능함   )
  
  
| URL 패턴 | 뷰 이름 | 템플릿 파일명 | 
| :--- | :---| :--- |
| /accounts/login/ | login() | registration/login.html | 
| /accounts/logout/ | logout() | registration/logged_out.html |  
| /accounts/password_change/ | password_change() | registratioin/password_change_form.html |  
| /acounts/password_change/done/ | password_change_done() | registration/password_change_done.html |  
| /accounts/password_reset/ | password_reset() | registration/password_reset_form.html, registration/password_reset_email.html, registration/password_reset_subject.txt |    
|/accounts/password_reset/done/ | password_reset_donne() | registration/password_reset_done.html |  
| /accounts/reset/ | password_reset_confirm() | registration/password_reset_confirm.html |  
| /accounts/reset/done/ | password_reset_complete() | registration/password_reset_complete.html|  
  
- - -   

  
### <font color="002469"> Setting.py 수정  </font>     
  
`LOGIN_URL`    
로그인 페이지로 리다이렉트시킬때 사용되는 URL.   
값을 지정하지 않으면 <b> /accounts/login/ </b> 을 기본 URL로 사용   
  
`LOGOUT_URL`  
로그아웃시킬때 사용되는 URL   
값을 지정하지 않으면, <b> /accounts/logout </b> 을 기본 URL로 사용.      

`LOGIN_REDIRECT_URL`  
장고의 기분 로그인 뷰인 contrib.auth.login() 뷰는 로그인 처리가 성공한 후에 next 파라미터로 지정한 URL로 리다이렉트시킴.  
만일 next 파라미타값이 없다면, 여기에 지정된 값으로 URL로 리다이렉트시킴.  
  
  
`INSTALLED_APPS` 부분에 `django.contrib.auth` 이 포함되어 있는지 확인.  
(INSTALLED_APPS에는 장고 실행시 작동되는 앱들이 작성되어 있다.)   
  
- - -  
  
  
### <font color="002469"> URLConf 설정 </font>     
  
  
<b>mysite/urls.py</b>   	
```python  
# 계정등록(Register)처리를 수행하는 뷰를 import  
from mysite.views import UserCreateView, UserCreateDoneTV 
  
urlpatterns = [
   ... 
    # 인증 URL
    path('account/', include('django.contrib.auth.urls')),
    path('account/register/', UserCreateView.as_view(), name='register'),
    path('account/register/done/', UserCreateDoneTV.as_view(), name='register_done'),
]
```   
  
  
- - -  
  
  
### <font color="002469"> 뷰 작성하기 </font>  
   
   
login() 등의 장고 auth 모듈에서 제공하는 뷰는 따로 코드를 작성할 필요가 없음.  
하지만, auth 모듈에 없는 뷰인 회원가입을 담당하는 `UserCreateView`와 `UserCreateDoneTV`를 작성해주어야 한다.  
   
   
<b>mysiate/views.py</b>  
```python  
from django.views.generic.edit import CreateView  #1 제네릭뷰 CreateView import  
from django.contrib.auth.forms import UserCreationForm #2 UserCreateForm import
from django.urls import reverse_lazy

class UserCreateView(CreateView):
    template_name = 'registration/register.html'
    form_class = UserCreationForm
    success_url = reverse_lazy('register_done')


class UserCreateDoneTV(TemplateView):
    template_name = 'registration/register_done.html'
```   
  
<b> 제네릭 뷰 `CreateView`를 import </b>   
이 뷰는 테이블의 레코드를 생성하기 위에 필요한 폼을 보여주고, 폼의 입력을 통해 테이블의 레코드를 생성해주는 역할을 담당.  
제네릭 뷰 중에서 테이블 변경 처리에 관련된 뷰를 편집용 제네릭 뷰라고 하는데, CreateView 외에 UpdateView, DeleteView, FormView가 있음.   
  
<b> UserCreateForm import </b>  
UserCreateForm은 User 모델 객체를 생성하기 위해 보여주는 폼(장고에서 기본적으로 제공됨. )  
   

  
- - -     
  
### <font color="002469"> 템플릿 작성하기 </font>    
     
      
      
- - -   
  
    
[전체 프로그램 소스](https://github.com/EunHyeJung/Blog-BookmarkApp/tree/master/blog)     
[참조](https://book.naver.com/bookdb/book_detail.nhn?bid=10801625)   
　　  
