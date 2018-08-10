---
layout: post
title:  "Django Many-to-one relationships"
date:   2018-08-10
author: EunHye Jung
categories: python
comment : true
tags:	Django 장고 파이썬 Python
cover:  "/assets/instacode.png"
---   
    
      
- - -      
   
[참조(장고 공식문서)](https://docs.djangoproject.com/ko/2.1/topics/db/examples/many_to_one/)   

- - -    
  
  
###  <font color = "#0E4D92"> Many-to-one relationships</font>    
  
_ _ _   
  
   
#### <font color="#212930"> 테스트를 위한 Reporter, Article 모델 생성  </font>     
  
* `many-to-one` 관계를 정의하기 위해서는, `ForeignKey`를 사용한다.   
    
  ```python   
    from django.db import models  

    class Reporter(models.Model):
        name = models.CharField(max_length = 30)
        age = models.IntegerField()
        email = models.EmailField()
    
    class Article(models.Model):
        headline = models.CharField(max_length = 100)
        pub_date = models.DateField()
        reporter = models.ForeignKey(Reporter, on_delete = models.CASCADE)
    
        class Meta:
            ordering = ('headline', )
  ```   
   
* 한명의 리포터(Reporter)는 여러개의 기사(Article)를 작성할 수 있다.  
  기사에는 리포터에 대한 정보가 담겨있다.  
  
  
#### <font color="#212930"> Reporter와 Article 데이터 저장하기  </font>     
  
* 2명의 리포터 데이터 저장    
  
  ```python   
   >>> r = Reporter(name = 'John Smith', age = 30, email = 'john@eaxmple.com')   
  >>> r.save()
  >>> r2 = Reporter(name = 'Paul Jones', age = 26, email = 'paul@example.com')
  >>> r2.save()
  ```   
   
   
*  기사 데이터 저장    
      
   ```python    
   >>> from datetime import
   >>> a = Artcle(id = None, headline = "This is a test", pub_date = date(2018, 7, 27, reporter = r))  # 외래키로 'John Smith' 리포터를 지정함  
   >>> a.save()
   >>> a.reporter.id
    1
   >>> a.reporter
   <Reporter : John Smith>
   ```   
  
  외래키 관계를 설정하기 전에, 객체(Reporter)를 반드시 저장(save)해야한다. 그렇지않으면 ValueError 발생.  
  
* 리포터 객체를 이용해서도 기사를 만들 수 있다.  
  
  ```python  
  >>> new_article = r.article_set.create(headline = "John's second storey", pub_date = date(2018, 08, 11))
  >>> new_article.reporter  
  <Reporter: John Smith>
  >>> new_article.reporter.id
  1
  ```  
  
  
#### <font color="#212930"> 모든 데이터 가져오기  </font>     
  
* 리포터 데이터 가져오기  
  
```python  
>>> Reporter.objects.all()
>>> Article.objects.all()
```  
  
  
#### <font color="#212930"> 필드값으로 데이터 추출하기  </font>     
  
  * 이름이 'John'인 리포터가 작성한 기사 가져오기  
  ```python  
  >>> Article.objects.filter(reporter__name = 'John')
  <QuerySet [<Article: John's second story>, <Article: This is a test>]>
  ```  
  
  
  * 이름이 'John'이고, 나이가 30세인 리포터가 작성한 기사 가져오기  
  ```python  
  >>> Article.objects.filter(reporter__name = 'John', reporter__age = 30)
  <QuerySet [<Article: John's second story>, <Article: This is a test>]>
  ```    
  
  * 리포터의 key값으로 데이터 가져오기  
  ```python  
  >>> Article.objects.filter(reporter__pk = 1)
  <QuerySet [<Article: John's second story>, <Article: This is a test>]>
  >>> Article.objects.filter(reporter = 1)
  <QuerySet [<Article: John's second story>, <Article: This is a test>]>
  ```    
  
  
  
  
