---
layout: post
title:  "Hackerrank-SQL(BASIC JOIN)"
date:   2018-11-21
author: EunHye Jung
categories: etc
comment : true
tags:	sql oracle
cover:  "/assets/instacode.png"
---   
   
     
- - -      
    
    
###  <font color = "#0E4D92"> Asian Population </font>    
   
[링크](https://www.hackerrank.com/challenges/asian-population/problem)   
   
CITY와 COUNTRY 테이블에서, 대륙명(CONTINENT)이 'Asia'인 인구수의 총합을 구할 것.  
NOTE : CITY의 CountryCode 칼럼과 COUNTRY의 code 칼럼은 서로 매칭되는 키 칼럼들이다.    
    
   
```sql  
SELECT SUM(CI.POPULATION)
FROM CITY CI, COUNTRY CT
WHERE CONTINENT = 'Asia' AND CI.COUNTRYCODE = CT.CODE;
```  
  
   
- - -    
    
    
###  <font color = "#0E4D92"> African Cities </font>    
     
[링크](https://www.hackerrank.com/challenges/african-cities/problem)  
     
CITY와 COUNTRY 테이블에서 대륙명(CONTINENT)이 'Africa'인 모든 도시명(CITY)을 출력할 것.  
NOTE : CITY의 CountryCode 칼럼과 COUNTRY의 code 칼럼은 서로 매칭되는 키 칼럼들이다.  

     
```sql  
SELECT CI.NAME
FROM CITY CI, COUNTRY CT
WHERE CI.COUNTRYCODE = CT.CODE AND CT.CONTINENT = 'Africa';
```      
    
   
- - -   
    
    
###  <font color = "#0E4D92"> Average Population of Each Continent </font>    
     
[링크](https://www.hackerrank.com/challenges/average-population-of-each-continent/problem)   
   
CITY와 COUNTRY 테이블에서, 모든 대륙명(CONTINENT)과 각각 도시의 인구의 평균값을 반올림해서 출력할 것.   
NOTE : CITY의 CountryCode 칼럼과 COUNTRY의 code 칼럼은 서로 매칭되는 키 칼럼들이다.   
   
```sql  
SELECT CT.CONTINENT, ROUND(AVG(CI.POPULATION) - 0.5)
FROM CITY CI, COUNTRY CT
WHERE CI.COUNTRYCODE = CT.CODE
GROUP BY CT.CONTINENT;
```    
    
   
