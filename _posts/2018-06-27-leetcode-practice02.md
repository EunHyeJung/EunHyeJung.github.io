---
layout: post
title:  "leetcode-771.Jewels and Stones"
date:   2018-06-27
author: EunHye Jung
categories: algorithm
tags:	algorithm leetcode
comment : true
cover:  "/assets/instacode.png"
---

## Leetcode 771.Jewels and Stones

### 문제	
	
[문제출저][source]	  
보석을 뜻하는 J 스트링이 주어지고, 당신이 가진 돌을 나타내는 S 문자열이 있다.   
문자열 S의 각각의 문자는 당신이 가진 돌의 종류이다.   
당신이 가진 돌중에 보석이 몇개인지 궁금함.    
J에 있는 문자는 각각 별개임.  그리고 J와 S에 있는 모든 문자(character)들은 문자임(?)   
문자는 대소문자 구분.    	
Example 1:

Input: J = "aA", S = "aAAbbbb"
Output: 3
Example 2:

Input: J = "z", S = "ZZ"
Output: 0

Note:

S and J will consist of letters and have length at most 50.
The characters in J are distinct.

	
- - -
	

### 풀이코드	
  		
  * 2중 for문을 이용해서 풀었다.   
    이럴 경우 시간복잡도가 문자열 S의 길이 X 문자열 J길이만큼 나온다.

    	
```
    public int numJewelsInStones(String J, String S) {
        int cnt = 0;
		for (int i = 0, in = S.length(); i < in; i++) {
			for (int j = 0, jn = J.length(); j < jn; j++) {
				if (S.charAt(i) == J.charAt(j)) {
					cnt++;
				}
			}
		}
		return cnt;
    }
```
  	
- - -
    
#### 다른 사람의 코드
* 정규표현식을 이용할 경우 한줄의 코드로 답을 구할 수 있었다.   
```
public int numJewelsInStones(String J, String S) {
    return S.replaceAll("[^" + J + "]", "").length();
}
```
```
public int numJewelsInStones(String J, String S) {
        int res = 0;
        Set setJ = new HashSet();
        for (char j: J.toCharArray()) setJ.add(j);
        for (char s: S.toCharArray()) if (setJ.contains(s)) res++;
        return res;
    }
```

- - -
	
#### 배운점	
* 정규표현식 **[^]**  
  대괄호 사이에 가장 첫번째 문자로 ^문자가 있을때, 그 문자 이후에 존재하는 문자들을 제외한 
  모든 문자와 일치 .   
	
	
    
[source]:   https://leetcode.com/problems/jewels-and-stones/description/