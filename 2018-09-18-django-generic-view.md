---
layout: post
title:  "Django Generic View"
date:   2018-09-18
author: EunHye Jung
categories: python
comment : true
tags:	Django 장고 파이썬 Python GenericView 
cover:  "/assets/instacode.png"
---  
   
### Django GenericView   
  
장고는 웹 프로그램 개발 시 공통적으로 사용하는 로직을 미리 만들어놓고 기본 클래스로 제공하고 있는데  
이것들을 <b>제네릭 뷰(Generic View)</b>라고 한다.  
제네릭 뷰의 종류와 각 제네릭뷰의 역할을 잘 이해해야 클래스형 뷰를 잘 다룰수 있다.  
  
#### <font color ="#1134A6"> Base View</font>   
  
`View`   
가장 기본이 되는 최상위 제네릭뷰, 다른 모든 제네릭 뷰들은 View의 하위 클래스.  
   
`TemplateView`  
템플릿이 주어지면 해당 템플릿을 렌더링.  
단순하게 화면에 보여줄 템플릿 파일을 처리하는 정도의 간단한 뷰   
  
ex) HomeView는 TemplateView를 상속받아, home.html 파일을 렌더링해서 화면에 보여주는 역할 담당.  
```python
class HomeVew(TemplateView):
	template_name = 'home.html'  
```  
  
`RedirectView`   
URL이 주어지면 해당 URL로 redirect 시켜주는 제네릭뷰.  
  
  
#### <font color ="#1134A6"> Generic Display View</font>   
  
`DetailView` : 객체 하나에 대한 상세한 정보를 보여줌.  
`ListView` : 조건에 맞는 여러 객체를 보여줌.  
  
#### <font color ="#1134A6"> Generic Edit View</font>   
  
`FormView`   
폼을 보여주기 위한 제네릭 뷰  
폼을 지정해주는 form_class와 이 폼을 렌더링 하는데 필요한 template_name 속성이 주요 속성들.  
폼 처리가 성공한 후 redirect url을 지정하는 success_url 속성도 필요함.  
  
`CreateView`    
새로운 레코드를 생성해서 테이블에 저장해주는 뷰, FormView의 기능을 포함하고 있음      
  
`UpdateView`   
테이블에 이미 있는 레코드를 수정해주는 뷰, FormView 기능 포함, 작업 대상 테이블로붵 폼을 만들어주며, 최종적으로는 수정된 레코드를 테이블에 저장     

`DeleteView`    
기존 객체를 삭제하기 위한 제네릭뷰  
CreateView, UpdateView와 달리 별도의 폼이 필요하지 않음.  
  
#### <font color ="#1134A6">Generic Date View</font>   
  
`YearArchiveView`   
`MonthArchiveView`   
`WeekArchiveView`   
`DayArchiveView`   
`TodayArchiveView`   
`DateDetailView`    

