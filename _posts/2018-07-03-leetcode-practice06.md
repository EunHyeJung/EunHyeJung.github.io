---
layout: post
title:  "Leetcode 819. Most Commmon Word"
date:   2018-07-03
author: EunHye Jung
categories: algorithm
tags:	algorithm bit leetcode java
comment : true
cover:  "/assets/instacode.png"
---
  
## 819. Most Commmon Word
  
[문제출저](https://leetcode.com/problems/most-common-word/description/)  
  
한 단락과 금지어 리스트가 주어질때, 금지어에 포함되지 않은 가장 빈도수가 많은 단어를 찾을것.  
금지어가 아닌건 적어도 하나있고, 답은 유일함!  
  
  
 금지어는 소문자로 주어지며 구두점이 없음. 단락에는 대소문자 다쓰임. 답은 소문자임   
 
 
 
 Note:    
   
1 <= paragraph.length <= 1000.  
1 <= banned.length <= 100.  
1 <= banned[i].length <= 10.  
The answer is unique, and written in lowercase (even if its occurrences in paragraph may have uppercase symbols, and even if it is a proper noun.)  
paragraph only consists of letters, spaces, or the punctuation symbols !?',;.  
Different words in paragraph are always separated by a space.  
There are no hyphens or hyphenated words.  
Words only consist of letters, never apostrophes or other punctuation symbols.  
 
   
- - -
    
### 풀이    
   
* 입력값은 단락과 금지어리스트, 출력은 금지어가 아닌 가장 빈도수가 많은 단어  
* 신경써야할 부분은  
  1) 단락은 대소문자를 다포함하지만, 금지어는 소문자로만 주어진다는것  
  2) 와 같은 구두점들이 단락에 포함된다는  
* 해결 방법은  
  1) 단락을 소문자로 바꿔주고 공백을 기준으로 단락에서 단어들을 뽑아낸다 -> toLowerCase(), split() 메서드 이용  
  2) 단어들의 빈도수를 체크하기 위해 Map<String,Intger>를 이용했다.  
  3) 단락에 있는 단어를 하나씩 금지어인지아닌지 확인해야하는데, 그 전에 정규표현식을 이용해서 소문자가 아닌것들은 다 제거해준다.  -> replaceAll() 메소드, 정규표현식 `[^a-z]` 이용.  
  4) 금지어가 아닌것들은 map에 해당 정보를 담아준 다음, 최대 빈도를 갖는 단어를 찾아내었다.  
  
  [소스코드](https://github.com/EunHyeJung/AlgorithmStudy/blob/master/Leetcode/Leetcode-819-Most-Common-Word.java)
  
  

### 알게된것   
* 정규표현식에서 `\pP`를 이용하면, 구두점 제거가 가능 [참고](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html)  
* Map에서 최대값(value)를 갖는 key값 구하기 [참고](https://docs.oracle.com/javase/9/docs/api/java/util/Collections.html)  
 `Collections.max(wordCounter.entrySet(), Map.Entry.comparingByValue()).getKey()`   
 
  
