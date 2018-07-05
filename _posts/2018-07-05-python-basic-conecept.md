---
layout: post
title:  "Python Basic Conecpt(2)"
date:   2018-07-05
author: EunHye Jung
categories: python
tags:	python
cover:  "/assets/instacode.png"
---
    
### 제어문, 반복문  
      
* 조건표현식 한줄에 적기   
  `조건문이_참인_경우 if 조건문 else 조건문이_거짓인_경우`    
      
  ex) message = "success" if score >= 60 else "failure"   
      
* 별찍기 (while문 이용)    
    
`  
  *
  **
  ***
  ****
`  
      
`  
    i = 0
    while True:
      i += 1
      if i > 5: break
      print ('*' * i)
`   
     
* 다양한 for문의 활용   
  
`
  a = [ (1,2), (3,4), (5,6) ]
  for (first, last) in a:
    print(first + last)
`   
  
  -> a리스트의 요소값이 튜플이기 때문에, 각각의 요소들이 자동으로 (first, last)라는 변수에 대입됨.   
     
* 리스트내포(List comprehension)   
  리스트 안에 for문을 포함 -> 좀 더 편리하고 직관적인 프로그램을 만들 수 있음.  
  ex1) 리스트의 각 요소에 3을 곱하기  
    
  `
     a = [ 1, 2, 3, 4 ]  
     result = [ num * 3 for num in a ]  
  `
    
  ex2) 리스트 내포를 이용하여 다음 문장에서 모음('aeiou')를 제거  
  ` Life is too short, you need python `  
     
  `  
    vowels = 'aeiou'  
    sentence = 'Life is too short, you need python'  
    ' '.join([a for a in sentence if a not in vowels])  
  `  
      
 
### 함수
   
* 여러 개의 입력을 받는 함수  
  
  `  
    def 함수이름(*매개변수):  
      <수행할 문장>    
      ...  
  `    
      
* 키워드 파라미터 kwargs   
  `**kwargs`는 모둔 key=value형태의 입력인수가 저장되는 딕셔너리 변수  
    
  ex)  
  `  
    def func(*args, **kwargs):
      pinrt(args)
      print(kwargs)
    
    func(1,2,3, name='foo', arg=3)  
  `    
    
* lambda  
  lambda는 함수를 생성할떄 사용하는 예약어로, def와 동일한 역할을 함.  
  보통 함수를 한줄로 간결하게 만들때 사용(def를 사용해야 할정도로 복잡하지 않거나, def를 사용할수 없는곳에 주로 사용)  
         
  `  
    lamda 매개변수1, 매개변수2, ... : 매개변수를 이용한 표현식  
  `   
       
  lambda는 def를 사용할 수 없는 곳에서도 사용할 수 있다!   
         
  `  
    myList = [ lambda a,b : a+b, lambda a,b : a*b ]
    myList
    myList[0](3,4)  # -> 7
  `   
     
   람다 표현식을 이용하면, 홀수,짝수를 판별하는 코드도 단 한줄로 작성할 수 있다!  
       
   `  
    is_odd = lambda x : True if x % 2 == 1 else False  
   `    
       
### 사용자 입력과 출력, 파일 읽고쓰기   
  
* input 사용: input으로 입력되는것은 모두 문자열로 취급됨.  
* 문자열 띄어쓰기는 콤마를 사용  
  ` print("life","is","too short")   # life is too short 가 출력됨.`  
    
* [파일 읽고쓰기](https://wikidocs.net/26)   

  
### 클래스  
  
* 파이썬은 메서드명으로 `__init__` 을 사용하여 생성자를 만든다.  
* 메서드의 첫번째 매개변수명은 관례적으로 `self`라는 이름을 사용한다. (호출한 객체 자신이 전달됨)  
  
    
### 모듈    
  
`모듈`이란 함수나 변수 또는 클래스를 모아놓은 파일   
  
* 모듈을 사용하기 위해서는 import 키워드를 사용한다.    
  `import 모듈이름`   
 import는 현재 디렉터리에 있는 파일이나 파이썬 라이브러리가 저장된 디렉터리에 있는 모듈만 불러올 수 있다!  
   
* 모듈 함수를 사용하는 또 다른 방법    
  `from 모듈이름 import 모듈함수`  
  
  
