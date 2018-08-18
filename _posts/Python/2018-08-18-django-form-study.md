---
layout: post
title:  "Django Formset, InlineFormSet, ModelForm"
date:   2018-08-18
author: EunHye Jung
categories: python
comment : true
tags:	Django 장고 파이썬 Python
cover:  "/assets/instacode.png"
---   
    
      
- - -        
     
[참고](https://docs.djangoproject.com/ko/2.1/topics/forms/modelforms/#specifying-widgets-to-use-in-the-form-with-widgets)   
   
- - -      
  
  


###  <font color = "#0E4D92"> Formset </font>      
   
  
```python
from django import forms

class ArticleForm(forms.Form):
	title = forms.CharField()
    pub_date = forms.DateField()
```   
  
  
만약에 사용자가 여러개의 기사들을 한번에 작성하기를 원한다면, 다음과 같이 <b>ArticleFormSet</b>을 생성하면 된다.    
    
    
```python  
from django.forms import formset_factory

ArticleFormSet = formset_factory(ArticleForm)
```      
  
위에서 <b>ArticleFormSet</b>이라는 formset을 만들었고, formset은 여러개의 폼을 만들 수 있도록 해준다.   
formset에서 만들어지는 form 형식을 아래와 같이 출력해볼 수 있다.   
  
  
```python  
formset = ArticleFormSet()
for form in formset:
	print(form.as_table())  
  
# <tr>
#    <th>  <label for = "id_form-0-title"> Title : </label>  </th>
#    <td>  <input type = "text" name = "form-0-title" id = "id_form-0-title">  </td>
# </tr>
# <tr>
#    <th>  <label for = "id_form-0-pub_date"> Pub date : </label>  </th>
#    <td>  <input type = "text" name = "form-0-pub_date" id = "id-form-0-pub_date">  </td>
# </tr>
```   
    
    
만약 폼의 개수를 늘리고 싶다면 파라미터로 `extra` 값을 넣어서 추가해준다. (기존적으로 formset_factory에서 extra의 디폴트값은 1)   
아래처럼 extra값을 2로 지정하면, 2개의 빈폼이 보여질것이다.  
   
```python
ArticleFormSet = formset_factory(Article, extra = 2)
```      
    
    
- - -  
   
   
####  <font color="#212930"> 초기데이터를 formset에 설정해주기  </font>
   
   
초기데이터는 폼셋이 어떻게 이용할것인지를 알려주는 가이드 역할을 해준다.  
위에서 extra의 값으로 폼의 개수를 정의해주었다.  
이것은 초기 데이터에서 생성하는 폼의 수 외에 추가로 몇개의 폼을 더 만들것인지를 알려주는것이다. 
  
아래는 초기데이터값을 세팅해주고 extra 값을 2로 생성하서 formset을 사용하는 예제 코드이다.  
  
  
```python  
import datetime
from django.forms import formset_factory
from myapp.forms import ArticleForm  
  
ArticleFormSet = formset_factory(ArticleForm, extra = 2)
fromset = ArticleFormSet(initial =[
	{ 'title' : 'Django is now open source',
      'pub_date' : datetime.date.today(). } 
])
  
for form in formset:
	print(form.as_table())
  
# <tr>
#    <th>  <label for = "id_form-0-title"> Title : </label>  </th>
#    <td>  <input type = "text" name = "form-0-title" value = "Django is now open source" id = "id_form-0-title">  </td>
# </tr>
# <tr>
#    <th>  <label for = "id_form-0-pub_date"> Pub date : </label>  </th>
#    <td>  <input type = "text" name = "form-0-pub_date" value = "2018-08-18" id = "id-form-0-pub_date">  </td>
# </tr>
# <tr>
#    <th>  <label for = "id_form-1-title"> Title : </label>  </th>
#    <td>  <input type = "text" name = "form-1-title"  id = "id_form-1-title">  </td>
# </tr>
# <tr>
#    <th>  <label for = "id_form-1-pub_date"> Pub date : </label>  </th>
#    <td>  <input type = "text" name = "form-1-pub_date"  id = "id-form-1-pub_date">  </td>
# </tr>
# <tr>
#    <th>  <label for = "id_form-2-title"> Title : </label>  </th>
#    <td>  <input type = "text" name = "form-2-title"  id = "id_form-2-title">  </td>
# </tr>
# <tr>
#    <th>  <label for = "id_form-2-pub_date"> Pub date : </label>  </th>
#    <td>  <input type = "text" name = "form-2-pub_date" id = "id-form-2-pub_date">  </td>
# </tr>
```   
  
    
전체 3개의 폼셋이 생성되는 것을 확인할 수 있다.  
하나는 초기데이터를 세팅하기 위한 폼이고 나머지는 2개의 추가폼인것이다.  
(초기데이터는 딕셔너리 형태로 전달된다)  
  
formset을 사용할때 초기값을 사용하는 경우, formset을 제출할때 초기에 세팅된값과 동일하게 전달해주어야
사용자에 의해 변경된 양식이 있는지 formset이 감지할 수 있다.  
ex)   
`ArticleFormSet(request.POST, initial = [ ... ])`  
    
    
- - -  
     
  
   
###  <font color = "#0E4D92"> Model formset </font>      
  
  
모델을 이용해서 폼을 생성할 수 있는 ModelForm이 있듯이 모델을 이용해서 Formset도 만들 수 있다.   
  
예제에서 사용될 모델들은 아래와 같음.  
  
  
```python  
from django.db import models
from django.froms import ModelForm

TITLE_CHOICES = (
	('MR', 'Mr.'),
    ('MRS', 'Mrs.'),
    ('MS', 'Ms.'),
)

class Author(models.Model):
	name = models.CharField(max_length = 100)
    title = models.CharField(max_length = 3, choices = TITLE_CHOICES)
    birth_date = models.DateField(blank = True, null = True)
    
    def __str__(self):
    	return self.name
        
class Book(models.Model):
	name = models.CharField(max_length = 100)
    author = models.ManyToManyField(Author)

```    
  
  
<b>Author</b> 모델을 사용해서 formset을 다음과 같이 만들어볼 수 있다.  
   
    
```python    
from django.forms import modelformset_factory
from myapp.models import Author

AuthorFormSet = modelformset_factory(Author, fields = ('name', 'title'))
```  
   
   
<b>fields</b>를 사용하면, 폼셋이 fields에 주어진 값들만 필드로 사용하도록 제한한다.  
반대로 특정 필드만 제외하고 싶을때는 아래와 같이 `exclue`값을 지정해주면 된다. 
  
  
```python   
AuthorFormSet = modelformset_factory(Author, exclue('birth_date', ))
```   
  
이제 모델 Author을 가지고 formset을 만들 수 있게 되었다. 만들어진 formset은 아래와 같이 확인해볼 수 있다.  
  
  
```python   
formset = AuthorFormSet()
print(formset)

# <input type="hidden" name="form-TOTAL_FORMS" value="1" id="id_form-TOTAL_FORMS">
# <input type="hidden" name="form-INITIAL_FORMS" value="0" id="id_form-INITIAL_FORMS">
# <input type="hidden" name="form-MAX_NUM_FORMS" id="id_form-MAX_NUM_FORMS">
# <tr>
#    <th>  <label for="id_form-0-name"> Name :  </label>  </th>
#    <td>  <input id="id_form-0-name" type="text" name="form-0-name" maxlength="100">  </td>
# </tr>
# <tr>
#    <th>  <label for="id_form-0-title"> Title :  </label>  </th>  
#    <td>  <select name = "form-0-title" id = "id_form-0-title">
#           <option value = "" selected>--------</option>
#           <option value="MR"> Mr. </option>
#           <option value="MRS"> Mrs. </option>
#           <option value="MS"> Ms. </option>
#         </select>   
#         <input type="hidden" name="form-0-id" id="id_form-0-id"> 
#   </td>      
# </tr>
```  
   
   
<b>modelformset_factory()</b>는 formset을 만들기 위해 <b>formset_factory()</b>를 사용한다. 이것은, model formset은 기본적인 formset의 연장선이라는것을 의미한다.  
    
    
#### <font color="#212930"> formset에 있는 객체(object)들 저장하기</font>        
   
  
formset에 있는 객체들을 저장할때는 `save()`메소드를 이용한다.  
```python  
formset = AuthorFormSet(request.POST)  # POST 데이터로 formset 객체 생성
instances = formset.save()
```  
   
   
`save()` 메소드는 데이터베이스에 저장된 객체들을 반환한다.  
  
  
- - -  
  
   
###  <font color = "#0E4D92"> Inline formsets </font>      
  
   
1:N 관계의 테이블을 기초로 폼을 만드는 경우, 1 테이블에 대한 폼을 메인폼이라 하고, N 테이블에 대한 폼을 인라인 폼셋이라고 한다.  

아래와 같이 작가와 책 모델이 있고, 한명의 작가가 여러 책을 작성할 수 있으니 책은 작가를 외래키로 지정하고 있다고 하자.  
  
  
```python  
from django.db import models

class Author(models.Model):
	name = models.CharField(max_length = 100)
    
class Book(models.Model):
	author = models.ForeignKey(Author, on_delete = models.CASCADE)
    title = models.CharField(max_length = 100)
```  
  
  
만약 특정 저자에 속한 책을 편집할 수 있는 formset을 만드려면 다음과 같이 작성하면 된다.  
  
  
```python  
from django.forms import inlineformset_factory
BookeFormSet = inlineformset_factory(Author, Book, fields = ('title', ))
author = Author.objects.get(name = 'Mike Royko')
formset = BookFormSet(instance = author)
```  

  
  
#### <font color="#212930"> inline formset 뷰(View)에서 사용하기 </font>    
  
  
```python  
def manage_book(request, author_id):
	author = Author.objects.get(pk = author_id)
    BookInlineFormset = inlineformset_factory(Author, Book ,fields = ('title',))
    if request.method == 'POST':
    	formset = BookInlineFormSet(request.POST, request.FILES, instance = author)
        if formset.is_valid():
        	formset.save()
            return HttpResponseRedirect(author.get_absolute_url())
    else:
    	formset = BookInlineFormSet(instance = author)
    return render(request, 'manage_books.html', { 'formset' : formset})
```  



  
