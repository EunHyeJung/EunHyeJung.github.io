---
layout: post
title:  "Sherlock and Anagrams"
date:   2018-07-04
author: EunHye Jung
categories: algorithm
tags:	algorithm string java hackerrank
comment : true
cover:  "/assets/instacode.png"
---
  
  
### Sherlock and Anagrams
 
  
### 문제 
  
[문제출저](https://www.hackerrank.com/challenges/sherlock-and-anagrams/problem)  
  
두 문자가 있고, 한 문자열에 있는 문자들을 재조합해서 다른 한문자열과 동일한 문자열을 만들 수 있다면 애너그램이다.  
문자열이 주어질때, 서로 아나그램인 문자열의 부분문자열 쌍의 수를 구하여라.  
예를 들어, s = mom이면, 아나그램인 쌍은 [[0], [2]], [[0,1],[1,2]]에 위치한 [m, m], [mo om]이다.  

  
  
- - -
  
  
### 풀이  
* 문자열에서 부분문자열들을 어떻게 추출할지, 또 부분문자열들에서 애너그램 쌍을 어떻게 찾을지 고민했다.  
* 우선, 문자열에서 부분문자열을 추출하는 방법은 subString() 메소드와 이중 for문을 이용했다.  
  
```
for(int subStrLength = 1, n = s.length(); subStrLength < n; subStrLength) {
	for(int stIdx = 0; stIdx < n; stIdx++) {
    	if(stIdx + subStrLength <= n) {
    		String subStr = s.subString(stIdx, stIdx + subStrLength);
        }
    }
}
```
 
 
* 애너그램은 당연히 두개의 문자열의 길이가 같아야 하므로, 안쪽 for문이 부분문자열을 추출할떄 그것을 리스트에 담아서  
  바깥 for문이 새롭게 시작하기 전에, 같은 길이에 속한 부분문자열들 중에 애너그램이 존재하는지 확인하였다.  
   
```
for(int subStrLength = 1, n = s.length(); subStrLength < n; subStrLength) {
	for(int stIdx = 0; stIdx < n; stIdx++) {
    	List<String> subsetList = new ArrayList<>();
    	if(stIdx + subStrLength <= n) {
    		subsetList.add(s.subString(stIdx, stIdx + subStrLength));
        }
    }
 
 	for(int idx = 0, size = subSetList.size(); idx < size; idx++) {
    	for(int compIdx = idx + 1; compIdx < size; compIdx++) {
        	if(isAnagrams(subSetList.get(idx), subSetList.get(compIdx))) {
            	cnt++;
            }
        }
    }
    
}
```
   
* 두 문자열이 애너그램인지 확인하는 방법은, 알파벳의 총개수(26)를 담는 char형 배열을 선언해두고,   
  각 문자열의 빈도수를 체크해준 다음, 두 개의 char배열을 비교하는 방법을 이용했다.  
    
  [전체소스](https://github.com/EunHyeJung/AlgorithmStudy/blob/master/Hackerrank/Sherlock-and-Anagrams.java)
    
   
    
- - -
