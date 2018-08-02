---
layout: post
title:  "Leetcode 32. Longest Valid Parentheses"
date:   2018-08-02
author: EunHye Jung
categories: algorithm
tags:	algorithm leetcode java
cover:  "/assets/instacode.png"
---  
    
   
### Leetcode 32. Longest Valid Parentheses   
  
[문제출저](https://leetcode.com/problems/longest-valid-parentheses/description/)  
   
오로지 `(`와 `)`를 포함하는 문자열이 주어질때, 가장 긴 유효한(valid) 괄호 부분문자열의 길이를 찾아낼것.     
      
      
<b> Example 1: </b>  
  
Input: ")()())"  
Output: 4   
Explanation: The longest valid parentheses substring is "()()   
    
    	
((()))   <- 이것두 유효한 괄호문자열이다.  
    
      
- - -     
  
  
## Leetcode Article   
   
   
[참조](https://leetcode.com/problems/longest-valid-parentheses/)
  
  
#### 접근법 1. Brute Force    
  
  
주어진 문자열에서 모든 가능한 짝수개의 부분문자열을 뽑아낸다.        
그런다음에, 스택을 이용해서 올바른 괄호인지 아닌지를 체크한다.            
   
만약에 주어진 문자열이 "((())"라면 나올 수 있는 부분문자열의 집합은 다음과 같을 것이다.  
        
((   
))   
()  
))  
((()  
(())  
    
열린괄호 '('를 만나면 스택에 넣는다. 
그리고 ')'를 만나게되면, 스택에서 '('를 뽑아낸다.   
만약 스택이 비어있는 경우나, 문자열끝까지 탐색하였음에도 스택이 비어있지 않는다은 경우라면     
이건 유효하지 않은것으로 판단한다.    
    
이런방식을 위에서 추출한 모든 부분문자열에 적용해서 가장 긴 유효한 괄호값을 찾아낸다.  
   
   
    
```java   
public boolean isValid(String s) {
	Stack<Character> stack = new Stack<Character>();
    for(int i = 0; i < s.length(); i++) {
    	if(s.charAt(i) == '(')) {
        	stack.push('(');
        } else if(!stack.empty() && stack.peek() == '(') {
        	stack.pop();
        } else {
        	return false;
        }
    }
    return stack.empty();
}

public int longestValidParentheses(String s) {
	int maxLen = 0;
    for(int i = 0; i < s.length(); i++) {
    	for(int j = i + 2; j <= length(); j+=2) {
        	if(isValid(s.substring(i, j))) {
            	maxLen = Math.max(maxLen, j - i);
            }
        }
    }
    return maxLen;
}
```   
   
   
   
<b> 복잡도 분석(Complexity Analysis) </b>     
  
* 시간복잡도 : O(n^3)  
  길이가 n인 문자열에서 모든 가능한 부분문자열을 추출하는데 O(n^2)만큼의 시간이 소요된다.  
  그리고 이것이 유효한 문자열인인지 체크하는데 O(n)만큼의 시간이 소요되므로 결과적으로 시간복잡독 O(n^3)이 나옴.    
* 공간복잡도 : O(n)   
   최대 n크기의 스택이 필요함.  
   
   
- - -    
   
   
#### 접근법 2. Dynamic Programming   
  
  
이 문제는 다이나믹 프로그래밍을 이용해서 풀 수 있다.  
dp[i]는 i로 끝나는 가장 긴 유효한 문자열의 길이가 된다.   
(여기서 i는 입력으로 주어진 문자열 str의 인덱스값)   
  
한가지 중요한점은 우리는 str.charAt(i)의 값이 `)`인 경우만 고려하면 된다는것이다.  
(유효한 문자열은 마지막엔 `)`로 끝나야하므로)  
그러므로 dp배열의 값은 ')'를 만날때만 업데이트된다.   
    
이제 `)`을 만나게 되어 dp값을 업데이트하는 경우를 고려해보자. 총 두가지 케이스를 고려할 수 있다.  
  
1) str[i] == ')'이고, str[i-1] == '('인 경우  ex:  ()   
   
   dp[i]의 값은 dp[i-2] + 2가 된다.  
   
2) str[i] == ')'이고 str[i-1] == ')'인 경우  ex : .. ))   
   <font color='blue'>)</font><font color='red'>)</font> 에서 <font color='blue'>)</font>까지 유효한 문자열이고, <font color='red'>)</font>가 유효한 문자열이라면, <font color='blue'>)</font>로 끝나는 유효한 문자열 전에 `(`가 있어야 한다.   
   그러므로 <font color='blue'>)</font>로 끝나는 부분문자열 앞에 `(`가 나오면, 우리는 <font color='blue'>)</font>로 끝나는 부분문자열의 길이에 2를 더해줘서 dp값을 업데이트 해준다.  
  또한, <font color='red'>(</font><font color='blue'>(...)</font><font color='red'>)</font>이전의 유효한 부분문자열의 길이도 잊지 않고 더해주어야한다.  -> `dp[i - dp[i - 1] - 2]`   
    
  
```java   
 public int longestValidParentheses(String s) {  
 	int maxLen = 0;
    int[] dp = new int[s.length()];
    
    for(int i = 1; i < s.length(); i++) {
    	if(s.charAt(i) == '(') {
        	if(s.charAt(i - 1) == '(') {
            	dp[i] = (i >= 2 ? dp[i - 2] : 0) + 2;
            } else if(i - dp[i - 1] > 0 && s.charAt(i - dp[i - 1] -1) == '(') {
            	dp[i] = dp[i - 1] + 2 + ((i - dp[i - 1] >=2 ? dp[i - dp[i - 1] - 2] : 0);
            }
            maxLen = Math.max(dp[i], maxLen);
        }
    }
    
 }
```   
  
  
<b> 복잡도 분석(Complexity Analysis) </b>    
* 시간복잡도 : O(n)  
  문자열 s의 길이를 한번만 순회하면서 dp배열 값을 채워주면 된다.  
* 공간복잡도 : O(n)   
  n크기의 dp 배열이 필요하다.   
   
   
   
   
- - -    
   
  
  
  
