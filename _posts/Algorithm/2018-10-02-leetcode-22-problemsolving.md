---
layout: post
title:  "Leetcode 22. Generate Parentheses"
date:   2018-10-12
author: EunHye Jung
categories: algorithm
tags:	algorithm leetcode java
cover:  "/assets/instacode.png"
---  
    
   
### Leetcode 22. Generate Parentheses   
  
[문제출저](https://leetcode.com/problems/generate-parentheses/)  
   
n이 입력될때, 올바른 괄호쌍의 조합들을 생성해내는 문제.     
      
      
만약에 n = 3이면, 유효한 괄호쌍의 조합들은 아래와 같이 나오게 된다.  
    
```   
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```   
      
- - -     
  
  
## Leetcode Article   
   
   
[참조(Leetcode Article)](https://leetcode.com/articles/generate-parentheses/)
  
  
#### 접근법 1. Brute Force   
   
'('와 ')' 문자들의 조합을 모두 생각해본다. (2^2n 개) 그리고 그 중 올바른 괄호쌍이 있는지 찾는다.  
모든 순열을 생성하기 위해, 재귀(recursion)를 이용한다.  
단순히 길이가 `(`와 `)`를 더해주면서 n길이의 괄호쌍을 만들어주면 된다.   

괄호가 올바른 형태인지 확인하기 위해 `balance`라는 변수를 사용한다.  
열린 괄호를 만나면 balance 값을 1 증가시켜주고, 닫힌 괄호를 만나면 1 감소시켜준다.  
balance 값이 0보다 작아지거나 최종적으로 0이 아니게 될경우에는 올바른 괄호쌍의 조합이 아니라고 판단한다.  
  
```java   
class Solution {
	public List<String> generateParenthesis(int n) {
    	List<String> combinations = new ArrayList();
        generateAll(new char[2 * n], 0, combinations);
        return combinations;
    }
    
    // 모든 괄호쌍의 조합들을 생성하는 함수
    public void generateAll(char[] current, int pos, List<String> result) {
    	if (pos == current.length) {
        	if (valid(current)) { // 유효한 괄호쌍의 조합이라면
            	result.add(new String(current));
            }
        } else {
        	  current[pos] = '(';
            generateAll(current, pos + 1, result);
            current[pos] = ')';
            generateAll(current, pos + 1, result);
        }
    }
    
    // 유효한 괄호쌍인지 체크하는 함수
	public boolean valid(char[] current) {
    	int balance = 0;
        for (chr c : current) {
        	if (c == '(') {
            	balance += 1 ;
            } else {
            	balance -= 1;
            }
            if (balance < 0) {
            	return false;
            }
		}
        return (balance == 0);
    }
}
```   
   
   
- - -    
  
  
#### 접근법 2. BackTracking   
      
    
접근1에서처럼 매번 `(`와 `)`를 더하면서 괄호쌍을 만들어나가는 대신에, 올바른 괄호쌍의 형태를 유지하고 있을때만 더해준다.  
이 방법을 이용하기 위해 현재 열린 괄호와 닫힌 괄호를 체크해준다.  
만약 현재 여는 괄호의 개수가 n보다 작은 상태라면 일단 여는 괄호를 추가한다.  
그리고 여는 괄호의 수만큼 닫힌 괄호도 필요하므로, 닫힌 괄호의 수가 여는 괄호의 수보다 작다면 닫힌 괄호를 추가해준다.  
   
```java  
class Solution {
	public List<String> generateParenthesis(int n) {
    	List<String> ans = new ArrayList<>();
        backtrack(ans, "", 0, 0, n);
        return ans;
    }
    
    public void backtrack(List<String> ans, String cur, int open, int close, int n) {
    	if(cur.length() == n * 2) {
        	ans.add(cur);
            return;
        }
        if (open < n) {
        	backtrack(ans, cur + "(", open + 1, close, n);
        } 
        if (close < open) {
        	backtrack(ans, cur + ")", open, close + 1, n);
        }
    }
 }
``` 
  
  
