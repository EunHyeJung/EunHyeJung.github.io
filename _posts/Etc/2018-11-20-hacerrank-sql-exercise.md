---
layout: post
title:  "Hackerrank-SQL(ADVANCED SELECT)"
date:   2018-11-20
author: EunHye Jung
categories: etc
comment : true
tags:	sql oracle
cover:  "/assets/instacode.png"
---   
   
- - -    
    
    
###  <font color = "#0E4D92"> Type Of Triangle </font>    
     
[링크](https://www.hackerrank.com/challenges/what-type-of-triangle/problem)  
     
TRIANGLES 테이블에서 3변을 나타내는 칼럼을 사용하여, 삼각형의 유형을 파악하는 쿼리를 작성.  
* Equilateral : 3개 면의 길이가 모두 동일한 삼각형  
* Isosceles : 2개 면의 길이가 동일한 삼각형  
* Scalene : 3개 면의 길이가 다른 삼각형   
* Not A Triangle : 3개의 면이 삼각형을 형성하지 않음.   

     
```sql  
SELECT CASE WHEN A + B <= C THEN 'Not A Triangle'
            WHEN A = B AND B = C THEN 'Equilateral'
            WHEN A = B OR B = C OR A = C THEN 'Isosceles'
            ELSE 'Scalene'
       END
FROM TRIANGLES ;
```      
    
<b>[ORACLE CASE](https://docs.oracle.com/cd/B19306_01/server.102/b14200/expressions004.htm)</b>     
CASE 문은 SQL에서 조건문을 이용할때 사용  
  
         
         
  
