---
layout: post
title:  "leetcode-461.Hamming Distance"
date:   2018-06-29
author: EunHye Jung
categories: algorithm
tags:	algorithm leetcode
comment : true
cover:  "/assets/instacode.png"
---
  
## Leetcode 461. Hamming Distance  
  
### 문제  
[문제출저](https://leetcode.com/problems/hamming-distance/description/)
  
두 정수(integer) 사이의 해밍거리는 비트값이 다른 위치의 개수를 뜻한다.  
x, y가 주어졌을때, 해밍거리를 계산하라.  
  
Note:
0 ≤ x, y < 2^31.

Example:

Input: x = 1, y = 4

Output: 2

Explanation:
1   (0 0 0 1)   
4   (0 1 0 0)   
　　↑ 　↑

The above arrows point to positions where the corresponding bits are different.
  
  
- - -
   
### 풀이코드	
* 2진수 비트수를 담는 int형 배열 두개를 가지고, 주어진 x,y값을 2진수르 변환한 후 해밍거리값을 계산했다.   
  
```
	public static final int N = 32;

	public int[] getBinary(int input) {
		int[] binary = new int[N];
		int idx = N - 1;
		while (input > 0) {
			if (input % 2 == 1) {
				binary[idx] = 1;
			}
			input /= 2;
			idx--;
		}
		return binary;

	}

	public int hammingDistance(int x, int y) {
		int[] xBinary = getBinary(x);
		int[] yBinary = getBinary(y);

		int distance = 0;
		for (int i = 0; i < N; i++) {
			if (xBinary[i] != yBinary[i]) {
				distance++;
			}
		}
		return distance;
	}
```
  

- - -
   
    
### 다른 사람의 코드   
* XOR연산을 수행한 후, Integer.bitCount()을 쓰니 1줄로 문제를 해결했다ㅇ0ㅇ...  
   
```
    public int hammingDistance(int x, int y) {
        return Integer.bitCount(x ^ y);
    }
```
   
* 역시 XOR연산을 이용하였지만, 비트연산을 통해 해밍거리를 계산했다.  
   
```
public int hammingDistance(int x, int y) {
    int xor = x ^ y, count = 0;
    for (int i=0;i<32;i++) count += (xor >> i) & 1;
    return count;
}
 ```
   
    
 
- - -
	    
### 공부할것
* 비트연산
  
