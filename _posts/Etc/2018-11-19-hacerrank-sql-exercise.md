---
layout: post
title:  "Hackerrank-SQL(BASIC SELECT)"
date:   2018-11-19
author: EunHye Jung
categories: etc
comment : true
tags:	sql oracle
cover:  "/assets/instacode.png"
---   
   
- - -    
    
    
###  <font color = "#0E4D92"> Revising the Select Query 1 </font>    
     
[링크](https://www.hackerrank.com/challenges/revising-the-select-query/problem)  
     
CITY 테이블로부터 인구(Population)가 100000보다 많고, 국가코드(CountryCode)가 USA인 모든 데이터들을 조회.   
     
```sql  
SELECT * FROM CITY WHERE POPULATION > 100000 AND COUNTRYCODE = 'USA';
```      
    
     
- - -   
    
    
###  <font color = "#0E4D92"> Revising the Select Query 2 </font>    
   
[링크](https://www.hackerrank.com/challenges/revising-the-select-query-2/problem)   
   
CITY 테이블로부터 인구(Population)가 120000보다 많고, 국가코드(CountryCode)가 USA인 모든 이름(Name)들을 조회.   
       
```sql  
SELECT NAME FROM CITY WHERE POPULATION > 120000 AND COUNTRYCODE = 'USA';
```      
   
   
- - -     
    
    
###  <font color = "#0E4D92"> Weather Observation Station3 </font>    
  
[링크](https://www.hackerrank.com/challenges/weather-observation-station-3/problem)  
  
STATION 테이블에서 ID값이 짝수인 CITY 칼럼을 조회 (단, 중복된 값은 제외)   
   
```sql  
SELECT DISTINCT CITY FROM STATION WHERE MOD(ID, 2) = 0; 
``` 
   
    
- - -     
    
    
###  <font color = "#0E4D92"> Weather Observation Station5 </font>    
    
[링크](https://www.hackerrank.com/challenges/weather-observation-station-5/problem)    
    
STATION 테이블에서 가장 긴 도시 이름과 가장 짧은 도시 이름과 각각의 길이를 구하라.  
만약 가장 긴 이름을 가지거나 가장 짧은 이름을 가진 도시가 여러개라면 알파벳 순으로 선택했을 때 먼저 나오는것을 구하라.   
     
```sql   
SELECT * FROM (
    SELECT CITY, LENGTH(CITY)
    FROM STATION
    ORDER BY LENGTH(CITY) DESC, CITY ASC
    ) 
WHERE ROWNUM = 1;

SELECT * FROM (
    SELECT CITY, LENGTH(CITY)
    FROM STATION
    ORDER BY LENGTH(CITY) ASC, CITY ASC
    ) 
WHERE ROWNUM = 1;
```   
   
    
- - -     
    
    
###  <font color = "#0E4D92"> Weather Observation Station6 </font>    
   
[링크](https://www.hackerrank.com/challenges/weather-observation-station-6/problem)   
     
STATION 테이블에서 도시이름(City)이 모음으로 시작하는것만 조회.  
중복없이 출력할 것.  
   
SOL1)         
```sql   
SELECT DISTINCT CITY 
FROM STATION
WHERE UPPER(SUBSTR(CITY, 1, 1)) IN ('A', 'E', 'I', 'O', 'U');
```  
  
SOL2)    
```sql  
SELECT DISTINCT CITY 
FROM STATION
WHERE REGEXP_LIKE(CITY, '^[AaIiEeOoUu]');
```      
   
   
- - -     
    
    
###  <font color = "#0E4D92"> Weather Observation Station7 </font>    
   
[링크](https://www.hackerrank.com/challenges/weather-observation-station-7/problem)   
   
STATION 테이블에서 도시 이름(City)이 모음으로 끝나는 것을 중복없이 조회할 것.   
      
```sql   
SELECT DISTINCT CITY 
FROM STATION
WHERE REGEXP_LIKE(UPPER(SUBSTR(CITY, -1)), '[AEIOU]');
```   
   
   
- - -     
    
    
###  <font color = "#0E4D92"> Higher Than 75 Marks </font>    
   
[링크](https://www.hackerrank.com/challenges/more-than-75-marks/problem)   
   
STUDNETS 테이블에서 점수가 75점보다 큰 학생들의 이름을 조회.  
이름에서 마지막 3문자를 기준으로 정렬하고, 만약 이름의 끝 3글자가 같은 학생이 있으면(ex: Bobby, Robby)   
ID를 기준으로 증가하는 순으로 정렬.   
  
```sql  
SELECT NAME FROM STUDENTS WHERE MARKS > 75
ORDER BY SUBSTR(NAME, -3) ASC, ID ASC;
```   
       
<b> [oracle substr](https://docs.oracle.com/cd/B19306_01/server.102/b14200/functions162.htm) </b>   
SUBSTR(문자열 OR 칼럼명, 시작위치, 끝위치) // 시작 위치는 1부터 시작    
ex1) SUBSTR('문자열', 3)  // 문자열의 3번째부터 끝까지 문자열 읽기  
ex2) SUBSTR('문자열', -4, 2) // 뒤에서 4번째부터 2개의 문자열 읽기   
     
- - -    
  
     
###  <font color = "#0E4D92"> Employee Names </font>    
  
[링크](https://www.hackerrank.com/challenges/name-of-employees/problem)    
     
Employee 테이블에서 모든 임직원들의 이름을 알파벳 순서대로 출력.   
     
```sql    
SELECT NAME FROM EMPLOYEE ORDER BY NAME;
```    
   
   
- - -  
  
     
###  <font color = "#0E4D92"> Employee Salaries </font>     
   
[링크](https://www.hackerrank.com/challenges/salary-of-employees/problem)   
    
EMPLOYEE 테이블에서 month 값이 10(달)보다 작고, 매달의 급여(Salary)가 2000달러보다 크고, 모든 임직원들의 이름을 조회.  
결과 값을 employee_id 오름차순으로 정렬할 것.  
   
```sql  
SELECT NAME FROM EMPLOYEE WHERE SALARY > 2000 AND MONTHS < 10 ORDER BY EMPLOYEE_ID;
```  
