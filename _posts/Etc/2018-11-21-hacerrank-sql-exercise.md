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
     
[문제링크](https://www.hackerrank.com/challenges/african-cities/problem)  
     
CITY와 COUNTRY 테이블에서 대륙명(CONTINENT)이 'Africa'인 모든 도시명(CITY)을 출력할 것.  
NOTE : CITY의 CountryCode 칼럼과 COUNTRY의 code 칼럼은 서로 매칭되는 키 칼럼들이다.  

     
```sql  
SELECT CI.NAME
FROM CITY CI, COUNTRY CT
WHERE CI.COUNTRYCODE = CT.CODE AND CT.CONTINENT = 'Africa';
```      
    
   
- - -   
    
    
###  <font color = "#0E4D92"> Average Population of Each Continent </font>    
     
[문제링크](https://www.hackerrank.com/challenges/average-population-of-each-continent/problem)   
   
CITY와 COUNTRY 테이블에서, 모든 대륙명(CONTINENT)과 각각 도시의 인구의 평균값을 반올림해서 출력할 것.   
NOTE : CITY의 CountryCode 칼럼과 COUNTRY의 code 칼럼은 서로 매칭되는 키 칼럼들이다.   
    
    
```sql  
SELECT CT.CONTINENT, ROUND(AVG(CI.POPULATION) - 0.5)
FROM CITY CI, COUNTRY CT
WHERE CI.COUNTRYCODE = CT.CODE
GROUP BY CT.CONTINENT;
```    
    
   
- - -   
    
    
###  <font color = "#0E4D92"> The Report </font>  
  
[문제링크](https://www.hackerrank.com/challenges/the-report/problem)    
     
Students와 Grades 테이블이 존재하고, Students 테이블은 ID, Name, Mark 3개의 칼럼들을 가지고 있다.  
Ketty는 Eve에게 Name, Grade, Marks 데이터를 포함하는 보고서를 작성하는 과제를 주었다.  
Ketty는 grade가 8보다 낮은 학생들의 이름은 표시되지 않기를 원하고, 보고서는 반드시 학점(grade)이 높은 순으로(내림차순으로) 정렬되어 있어야 한다.   
만약 등급이 8~10인 학생들 중 등급이 같은 학생이 있다면, 이름을 알파벳 순으로 출력해야 한다.  
그리고 만약 등급이 8보다 작다면 이름을 NULL 값으로 표시하여 출력하여야 한다.  
만약 등급이 8보다 작은 (1~7) 학생들 중 같은 등급을 가진 학생들이 있다면 마킹값(marks)이 작은것부터 (오름차순으로) 출력하면 된다. 
    
    
```sql  
SELECT CASE WHEN G.GRADE <= 7 THEN 'NULL' ELSE S.NAME END, G.GRADE, S.MARKS
FROM STUDENTS S, GRADES G
WHERE G.MIN_MARK <= S.MARKS AND S.MARKS <= G.MAX_MARK 
ORDER BY G.GRADE DESC,
         CASE WHEN G.GRADE > 7 THEN S.NAME END ASC,
         CASE WHEN G.GRADE <= 7 THEN S.MARKS END ASC;
```   
    
     
- - -   
    
   
###  <font color = "#0E4D92"> Top Competitors </font>  
  
[문제링크](https://www.hackerrank.com/challenges/full-score/problem)    
     
Julia는 코딩테스트를 시행하는 작업을 끝냈다. 그녀가 리더보드를 조합하는것을 도와주어야한다.  
둘 이상의 챌린지에서 전체 점수(full scores)를 받은 참여자들의 아이디(hacker_id)와 이름(name)을 출력하는 쿼리를 작성해야 한다.  
참여자가 전체 점수를 얻은 챌린지수가 많은 순으로(내림차순)으로 정렬하여야 하며,  
같은 횟수를 가진 참여자가 있다면 hacer_id가 증가하는 순서대로 정렬하여야 한다.  
테이블은 Hackers, Difficulty, Challenges 총 3개가 존재한다.  
   
Hackers : hacker_id(참여자 아이디), name(이름) 필드를 가진다.  
Difficulty : difficulty_level(챌린지의 난이도 레벨), score(점수) 필드를 가진다.  
Challenges : challenge_id(챌린지 아이디), hacker_id(챌린지를 만든 사람의 아이디), difficulty_level(난이도 레벨) 필드를 가진다.  
Submissions : submission_id(제출 아이디), hacker_id(제출한 사람의 ID), challenge_id(제출된 첼린지의 id), score(제출 점수) 필드를 가진다.  
   
```sql
SELECT H.HACKER_ID, H.NAME
FROM
    SUBMISSIONS S
    INNER JOIN CHALLENGES C ON S.CHALLENGE_ID = C.CHALLENGE_ID
    INNER JOIN DIFFICULTY D ON C.DIFFICULTY_LEVEL = D.DIFFICULTY_LEVEL
    INNER JOIN HACKERS H ON S.HACKER_ID = H.HACKER_ID
WHERE
    S.SCORE = D.SCORE
GROUP BY
    H.HACKER_ID, H.NAME
HAVING COUNT(S.HACKER_ID) > 1
ORDER BY COUNT(S.HACKER_ID) DESC, H.HACKER_ID ASC;
```   
     
<b> INNER JOIN </b>  
두 테이블을 조인할 때, 조인 조건에 부합되는 데이터들만 가져옴. (교집합이라고 생각하면 됨)  
  
INNER JOIN 기본 구문  
```sql    
SELECT <칼럼 목록>
FROM <첫번째 테이블>
  INNER JOIN <두번째 테이블>
  ON <조인될 조건>
[WHERE 검색조건]  
```    
    
     
- - -   
    
   
