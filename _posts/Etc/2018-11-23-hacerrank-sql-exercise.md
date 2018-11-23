---
layout: post
title:  "Hackerrank-SQL(Aggregation)"
date:   2018-11-23
author: EunHye Jung
categories: etc
comment : true
tags:	sql oracle
cover:  "/assets/instacode.png"
---   
    
    
###  <font color = "#0E4D92"> Revising Aggregations - The Sum Function </font>    
   
[문제링크](https://www.hackerrank.com/challenges/revising-aggregations-sum/problem)   
   
CITY 테이블에서 지역이 California인 모든 도시들의 인구수를 구할것.  
    
   
```sql  
SELECT SUM(POPULATION)
FROM CITY
WHERE DISTRICT = 'California';
```  
  
    
- - -   
  
    
###  <font color = "#0E4D92"> Average Population </font>    
   
[문제링크](https://www.hackerrank.com/challenges/average-population/problem)   
   
CITY 테이블에서 모든 도시에 대한 평균인구를 정수형으로 반올림하여 구할것.   
    
```sql  
SELECT ROUND(AVG(POPULATION), 0)
FROM CITY
```  
  
    
- - -   
  
    
###  <font color = "#0E4D92"> Population Density Difference </font>    
  
[문제링크] (https://www.hackerrank.com/challenges/population-density-difference/problem)  
   
CITY테이블에서 인구의 최대값과 최소값의 차이를 구할것.  
  
```sql  
SELECT (MAX(POPULATION) - MIN(POPULATION))
FROM CITY;
```  
   
   
- - -   
  
    
###  <font color = "#0E4D92"> Top Earners </font>    
  
[문제링크] (https://www.hackerrank.com/challenges/earnings-of-employees/problem)  
   
직원의 전체 급여를 salary 값과 months값을 곱하는것으로 정의했다.  
직원들중 가장 높은 전체 급여를 받은 직원의 전체 급여와 몇명이 최대 급여를 받았는지를 구하는 쿼리를 작성할것.  
EMPLOYEE 테이블은 employee_id, name, months, salary 칼럼을 가지고 있다.  
  
    
```sql   
SELECT TOP(1) SALARY * MONTHS EARNINGS, COUNT(*)
FROM EMPLOYEE
GROUP BY SALARY * MONTHS
ORDER BY SALARY * MONTHS DESC;
```   
      
  
<b> MSSQL - TOP </b>  
SELECT TOP절은 반환받은 레코드의 개수를 지정하여 받고 싶을때 사용한다.
(MYSQL의 LIMIT와 ORACLE의 ROWNUM과 유사한 개념)   
- 사용법  
  ```  
  SELECT TOP 숫자|PERCENT 열이름
  FROM 테이블이름
  WHERE 조건;  
  ```  
      
   
- - -   
   
    
###  <font color = "#0E4D92"> Weather Observation Station 2 </font>     
   
[문제링크](https://www.hackerrank.com/challenges/weather-observation-station-2/problem)  
    
STATION 테이블에서 다음 두개의 값을 조회하는 쿼리값을 작성.  
1. LAT_N의 모든 값의 합을 소수점 둘째자리까지 반올림해서 출력.  
2. LONG_W의 모든 값의 합을 소수점 둘째자리까지 반올림해서 출력.  
    
SOL1)  
```sql  
SELECT FORMAT(ROUND(SUM(LAT_N), 2), '#.00'), 
       FORMAT(ROUND(SUM(LONG_W), 2), '#.00')
FROM STATION
```  
   
SOL2)
```sql
SELECT CAST(SUM(LAT_N) AS DECIMAL(10, 2)),
       CAST(SUM(LONG_W) AS DECIMAL(10, 2))
FROM STATION;  
```        
<b> [MSSQL-CAST 및 CONVERT](https://docs.microsoft.com/ko-kr/sql/t-sql/functions/cast-and-convert-transact-sql?view=sql-server-2017) </b>   
데이터 형식의 식을 다른 데이터 형식으로 변환할때 사용.  
사용형식  
```sql
--- CAST Syntax;
CAST ( expression AS data_type [(length)] )
--- CONVERT Syntax;
CONVERT ( data_type [(length)], expression[, style] )
```  
  
<b> [MSSQL-FORMAT](https://docs.microsoft.com/ko-kr/sql/t-sql/functions/format-transact-sql?view=sql-server-2017)</b>   
    
   
- - -   
   
   
###  <font color = "#0E4D92"> Weather Observation Station 13 </font>     
   
[문제링크](https://www.hackerrank.com/challenges/weather-observation-station-13/problem)  
   
STATION 테이블로부터 LAT값이 38.7880보다 크고, 137.2345보다 작은 Northern Latitude(LAT_N)의 합을 구하는 쿼리를 작성.  
(소수점 4째자리까지 잘라서 출력)  
   
```sql   
SELECT CAST(SUM(LAT_N) AS DECIMAL(10,4))
FROM STATION
WHERE LAT_N > 38.7880 AND LAT_N < 137.2345;
```
   
    
- - -   
    
    
###  <font color = "#0E4D92"> Weather Observation Station 14 </font>     
   
[문제링크](https://www.hackerrank.com/challenges/weather-observation-station-14/problem)  
   
STATION 테이블에서 LAT_N값이 137.2345보다 작은 LAT_N 값중 가장 큰 값을 소수점 4째자리까지 잘러서 출력.   
   
```sql  
SELECT CAST(MAX(LAT_N) AS DECIMAL(10,4))
FROM STATION
WHERE LAT_N < 137.2345;
```   
   
   
---   
   
      
###  <font color = "#0E4D92"> Weather Observation Station 15 </font>     
   
[문제링크](https://www.hackerrank.com/challenges/weather-observation-station-15/problem)  
     
STATION 테이블에서 137.2345보다 작으면서 최대인 LAT_N 값을 가진 레코드의 LONG_W 값을 출력.  
(소수점 4자리까지 잘라서 출력)  
      
```sql  
SELECT CAST(LONG_W AS DECIMAL(10,4))
FROM STATION
WHERE LAT_N = (SELECT MAX(LAT_N) FROM STATION WHERE LAT_N < 137.2345);
```   
    
    
- - -   
   
   
###  <font color = "#0E4D92"> Weather Observation Station 16 </font>     
   
[문제링크](https://www.hackerrank.com/challenges/weather-observation-station-16/problem)    
    
STATION 테이블에서 LAT_N 값이 38.7780보다 큰 값들중 가장 작은 LAT_N 값을 출력.  
(소수점 4자리까지 잘라서 출력)   
   
```sql   
SELECT CAST(MIN(LAT_N) AS DECIMAL(10, 4))
FROM STATION
WHERE LAT_N > 38.7780;
```   
    
    
- - -   
   
   
###  <font color = "#0E4D92"> Weather Observation Station 18 </font>     
   
[문제링크](https://www.hackerrank.com/challenges/weather-observation-station-18/problem)    
      
2차원상에 P1(a, b)와 P2(a, b) 두 점이 있다고 고려해보자. 
   
* a는 Northern Latitude(LAT_N)의 최소값.    
* b는 Western Longitude(LONG_W)의 최소값. 
* c는 Northern Latitude(LAT_N)의 최대값.  
* d는 Western Longitude(LONG_W)의 최대값. 

두점 P1과 P2의 [맨하탄 거리(Manhattan Distance)](https://xlinux.nist.gov/dads/HTML/manhattanDistance.html)를 구하여 소수점 4자리까지 표시하는 쿼리작성.  
   
```sql   
SELECT CAST(ABS(SUB_S.A - SUB_S.C) + ABS(SUB_S.B - SUB_S.D) AS DECIMAL(10, 4))
FROM 
(SELECT 
    MIN(LAT_N) AS A, MIN(LONG_W) AS B, MAX(LAT_N) AS C, MAX(LONG_W) AS D
    FROM STATION
) SUB_S;
```   
    
<b> Inline View (From절 Subquery) </b>  
FROM절에 오는 서브쿼리.  
FROM절에서 원하는 데이터를 조회하여 가상의 집합을 만들어 조인을 수행하거나 가상의 집합을 다시 조회할 때 사용.  
[참고](http://www.gurubee.net/lecture/1505)   
     
    
- - -  
   
   
###  <font color = "#0E4D92"> Weather Observation Station 19 </font>     
   
[문제링크](https://www.hackerrank.com/challenges/weather-observation-station-19/problem)    
    
STATION 테이블에서 LAT_N 값의 최소값과 최대값을 a,b로 정의하고, LONG_W 값의 최소값과 최대값을 c, d로 정의할 때,  
두점 P(a, c), P(b, d)사이의 [유클리디안 거리(Eculidean Distance)](https://en.wikipedia.org/wiki/Euclidean_distance)를 구하는 쿼리작성.   
   
```sql   
SELECT CAST(SQRT(POWER(SUB_S.A - SUB_S.C, 2) + 
                 POWER(SUB_S.B - SUB_S.D, 2)) 
            AS DECIMAL(10, 4))
FROM
(
    SELECT MIN(LAT_N) A, MIN(LONG_W) B, MAX(LAT_N) C, MAX(LONG_W) D
    FROM STATION
) AS SUB_S;
```  
    
   
- - -   
   
   
   
