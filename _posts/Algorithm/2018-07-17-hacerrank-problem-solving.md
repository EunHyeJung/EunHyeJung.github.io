---
layout: post
title:  "hackerrank-funny-string"
date:   2018-07-17
author: EunHye Jung
categories: algorithm
tags:	algorithm string java hackerrank
comment : true
cover:  "/assets/instacode.png"
---
   
　  
   
### Funny String   
    
    
[문제출저](https://www.hackerrank.com/challenges/funny-string/problem)  
  
주어진 문자열이 웃긴(funny) 문자열인지 아닌지를 판단하는 코드 작성.  
문자열이 웃긴 문자열인지 아닌지를 결정하기 위해, 주어진 문자열을 뒤집은 문자열이 필요하다. (abc라면 cba).   
각 문자열의 문자들을 방문하면서 인접한 문자들의 아스키코드값의 차이를 비교한다.  
만약 절대값 차이가 두 문자열(입력문자열, 뒤집어진 입력문자열)이 같다면 그 문자열은 웃긴 문자열이 된다.   
    
    
- - - 
    
    
### 풀이
  
* 입력 문자열과 뒤집은 문자열의 문자를 추출하기 위한 인덱스 i, j를 이용한다.  
* i는 0부터 시작해서 (문자열의 길이 -1)까지 오름차순으로 문자를 추출하고,   
  j는 (문자열의 길이 -1)부터 1까지 내림차순으로 문자를 추출한다.  
  (기존의 문자열뒤에서부터 조회한다면 뒤집은 문자열을 조회하는 것이된다!)  
* 인접한 문자열의 아스키코드의 차이의 절대값을 구한 다음, 비교연산을 통해 문제를 해결 할 수 있다.  
  
  
<b> 코드 </b>  
   
```
    public  boolean isFunnyStr(String str) {
        for (int i = 0, n = str.length(), j = n - 1; i < n - 1 && j > 0; i++, j--) {
            if (Math.abs(str.charAt(i + 1) - str.charAt(i)) != Math.abs(str.charAt(j) - str.charAt(j - 1))) {
                return false;
            }
        }
        return true;
    }
```
   
　   
 　  
