---
layout: post
title:  "Python-Problem-Solving-String-01"
date:   2018-07-13
author: EunHye Jung
categories: python
tags:	python
cover:  "/assets/instacode.png"
---  
  
  


### String Split and Join  
 
[문제출저] (https://www.hackerrank.com/challenges/python-string-split-and-join/problem)  
  
* <b>풀이코드  </b>   
    
```   
def split_and_join(line):
    return "-".join(line.split())
```   
    
    
- - -  
    
### What's your name ?
 
[문제출저] (https://www.hackerrank.com/challenges/whats-your-name/problem)  
  
* <b>풀이코드  </b>   
    
```   
def print_full_name(a, b):
    print("Hello %s %s! You just delved into python." %(a, b)) 
```   
   
* <b>다른사람의 풀이코드</b>  
   
```  
def print_full_name(a, b):
    print("Hello {0} {1}! You just delved into python.".format(a, b))

```  
     
    
- - -  
      
### Mutations   
   
[문제출저] (https://www.hackerrank.com/challenges/python-mutations/problem)
    
파이썬에서 리스트(list)는 변경가능하고, 튜플(tuple)은 불가능하다.   
문자열을 입력받았는데, 입력받은 약간 변경하고 싶다고 하자.  
  
>> String = "abracadabra"    
 
문자열에서 특정 문자값을 출력하려면 인덱스값으로 접근이 가능하다.  
  
>> print string[5]
a  
  
만약, 인덱스값을 가지고 새로운 값으로 할당하려하면 에러가 발생한다.  
  
>> string[5] = 'k' 
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignmen
  
어떻게 이문제를 해결할 수 있을까?
 1) 문자열을 리스트로 바꾼 후 값을 변경.  
  
    >> string = abracadabra"
    >> l = list(string)
    >> l[5] = 'k'
    >> string = ''.join(l)
    >> print string  
   
 2) 문자열 슬라이싱과 조인을 이용.  
  
 	>> string = string[:5] + "k" + string[6:]
 	>> print string
 	abrakdabra
    
   
- - -  
   
### Find a string   
   
[문제출저](https://www.hackerrank.com/challenges/find-a-string/problem)  
   
사용자가 문자열(string)과 부분문자열(substring)을 입력할때, 부분문자열이 문자열에서 몇번 나왔는지를 출력. 
Note : 문자열은 대소문자 구분함!  
   
* <b>풀이코드  </b>   
    
```   

```   
   
   
- - -  
   
### Text Wrap   
   
[문제출저](https://www.hackerrank.com/challenges/text-wrap/problem)
    
문제)문자열 S와 너비(?)  w가 주어졌을대, 문자열은 s길이만큼 잘라서 출력  
    
* <b>풀이코드  </b>   
    
```   
def wrap(string, max_width):
    idx = 0
    length = len(string)
    res = ''
    while idx + max_width < length:
        res += (string[idx:idx+max_width] + "\n");
        idx += max_width

    res += string[idx:]
    return res
```   
   
* <b>다른 사람의 풀이코드</b>  
   
```
def wrap(string, max_width):
    res = ''
    for i in range(0, len(string) + 1, max_width):
        res += (string[i:i+max_width] + "\n")
    return res
	
```
  
* <b> 학습내용 </b>
  ` range([start,] stop [,step])`   
   : range는 연속적인 숫자(정수)를 만들어주며, 반복문에서 많이 사용됨!  
   : 반복을 시작할 처음 숫자, 반복 마지막 숫자(이 숫자는 포함안됨), 연속된 숫자들의 차이  
   
   
- - -   
   
### String Validators  
   
[문제출저](https://www.hackerrank.com/challenges/string-validators/problem)  
   
파이썬은 기본 데이터를 위한 문자열 검증 방법이 내장되어 있다.  
  
`str.isalnum()`: 문자열이 알파벳 혹은 숫자로 구성되어 있는지 체크 (a-z, A-Z, 0-9)    
`str.isalpha()` : 문자열이 알파벳으로 이루어져있는지 체크 (a-z, A-Z)    
`str.isdigit()` : 문자열이 숫자로 구성되어 있는지 체크 (0-9)   
`str.islower()` : 문자열이 소문자로 구성되어있는지 체크 (a-z)  
`str.isupper()` : 문자열이 대문자로 구성되어있는지 체크 (A-Z)   
   
   
- - -
   
### Captialize!  
  
[문제출저](https://www.hackerrank.com/challenges/capitalize/problem)    
   
문제) 여권에서 성과 이름의 첫글자는 대문자로 시작되어야함.  
이름을 입력받으면, 여권에서처럼 올바르게 성과 이름의 첫글자가 대문자로 시작되도록 변경할것.  
   
* <b>다른 사람의 코드</b>    
  
```
      s = ' '.join(map(str.capitalize, s.split(' ')))
```
  
* <b> 학습내용 </b>  
  `map(f, iterative)`   
  함수 f와, 반복가능한(iterable) 자료형을 입력으로 받음.  
  map은 입력받은 자료형의 각 요소가 함수 f에 의해 수행된 결과를 묶어서 리턴하는 함수.  
  [참조](https://wikidocs.net/32)   
  　
  　
　












