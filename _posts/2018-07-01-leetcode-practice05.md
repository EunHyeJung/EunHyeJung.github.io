---
layout: post
title:  "Leetcode 476. Number Complement"
date:   2018-07-01
author: EunHye Jung
categories: algorithm
tags:	algorithm bit leetcode java
comment : true
cover:  "/assets/instacode.png"
---
  
## 476. Number Complement   
  
[문제출저](https://leetcode.com/problems/number-complement/description/)  
  
양의 정수가 주어졌을때, 결과는 그것의 보수가 된다. 보수 전략은 이진수의 비트를 뒤집는것이다.  
Note :  
1. 주어진 정수는 32비트 부호있는 정수의 범위임을 보장하다.
2. 정수의 이진표현에서 선행 0비트가 없다고 가정할 수 있다.  

Example 1:
Input: 5
Output: 2
Explanation: The binary representation of 5 is 101 (no leading zero bits), and its complement is 010. So you need to output 2.
  
Example 2:
Input: 1
Output: 0
Explanation: The binary representation of 1 is 1 (no leading zero bits), and its complement is 0. So you need to output 0.
  
   
- - -
    
### 풀이코드    
   
* 10진수 num을 2진수로 표현하는 방법은 num이 0이 될때까지 2로 나눠주면서 2로나눈 나머지 값을 이어주면 된다.  
```
StringBuffer binaryNumSb = new StringBuffer();
while(num > 0) {
	binrayNumSb.append(num % 2);
	num /= 2;
}
```
   
* 보수가 이진수의 비트를 뒤집는 방법이므로 10진수를 2진수로 만드느 방법을 거꾸로 적용시켜서 문제를 해결했다. 
 ```
    public int findComplement(int num) {
		int i = 0, res = 0;
		while (num > 0) {
			res = res + ((num % 2 == 1 ? 0 : 1) * (int) Math.pow(2, i++));
			num /= 2;
		}
		return res;        
    }
```
  
  
### 다른 사람의 코드  (비트연산 이용)
```
      public int findComplement(int num) {
            int bits = 0;
            int n = num;
            while (n > 0) {
                n >>= 1;
                bits++;
            }
            return ~num & (1 << bits) - 1;
        }
```
   
### 참고  
* 시프트연산자 **>>**
   n >> i : n의 비트값을 i만큼 오른쪽으로 이동시킴, n / 2^(i)와 같은 결과를 가짐.  
   ~ : Not 연산자
