---
layout: post
title:  "비트 조작(Bit Manipulation)"
date:   2018-07-01
author: EunHye Jung
categories: java
tags:	java 비트조작 Bit
comment : true
cover:  "/assets/instacode.png"
---
   
### 비트 조작 (Bit Manupulation)   
 <table cellspacing="0" cellpadding="0">
  <tr>
    <td> 0110 + 0110</td><td> 0110 ＊ 2와 같다 = (0110 << 1)  = 0110을 왼쪽으로 1비트만큼 시프트</td><td>1100</td>
  </tr>
  <tr class="even">
    <td> 0100 ＊ 0011 </td><td> 0100은 4와 같으므로, 0011에 4를 곱하면 답을 얻을 수 있다.  
                               2^n으로 곱하는것은 n만큼 왼쪽으로 시프트하는것과 같음,    
                               -> 0011을 왼쪽으로 두 비트 시프트하면됨. (0011<<2)  </td><td>1100</td>
  </tr>
  <tr>
    <td> 1101 ^ (~1101) </td><td>어떤비트를 NOT한 값과 그비트를 XOR하면 항상 1이다. 즉, a^(~a)는 모든 비트가 1</td><td>1111</td>
  </tr>
  <tr class="even">
    <td> 1101 & (~-0 << 2) </td><td> ~0은 모든 비트가 1이다.  
                                   그 값을 왼쪽으로 n번 시프트하면 1이 빠져나간 자리에, n개의 0이 남게된다.  
                                   따라서 그 결과를 x와 ANd하게 되면, x의 우측 n개비트가 0이됨.   
                                   -> x & (~0 << n)는 x의 우측 n개 비트를 0으로 만든다. </td><td>10000</td>
  </tr>
</table>
   
- - -
   

### 비트조작시 참고할 내용  
  
0s : 모든 비트가 0인 값, 
1s : 모든 비트가 1인 값  
  
<table>
<tr>
<td> x ^ 0s = x </td>  <td> x & 0s = 0</td> <td> x | 0s = x</td>
</tr>
<tr>
<td> x ^ 1s = ~x </td> <td> x & 1s = x </td> <td> x | 1s = 1s </td>
</tr>
<tr>
<td> x ^ x = 0 </td> <td> x & x = x</td> <td> x | x = x</td>
</tr>
</table>

   

_ _ _
   
### 일작적인 비트 작업들   
   
#### Get : 특정 비트 값 얻어내기  
1을 i만큼 왼쪽으로 시프트하여, 그 값을 num과 AND함.
-> i번째 비트를 제외한 모든 비트가 지워짐 -> 그 값을 0과 비교.  
-> 0이 아니라면, i번째 비트값은 1이고, 0이면 i번째 비트값은 0.  
   
```
	boolean getBit(int num, int i) {
		return ((num & (1 << i)) != 0);
	}
```
   
#### Set : 특징 비트값 1로 만들기   
1을 i만큼 왼쪽으로 시프트하여, 그 값을 num과 OR연산함. 
-> i번째 값만 1로 바꿈 -> 다른 비트들은 0과 OR되므로 원래의 값 유지됨.  
   
```
int setBit(int num, int i) {
		return num | (1 << i);
}
```
   
#### Clear: 특정비트값 지우기   
1을 i만큼 왼쪽으로 시프트함. -> NOT 연산 -> 그 다음 num과 AND 연산 수행.  
-> i번째 비트만 지워지고 나머지 비트는 그대로 일것임.  
   
```
int clearBit(int num, int i) {
		int mask = ~(1 << i);
		return num & mask;
}
```
   
#### Update : 특정 비트 값 갱신하기  
setBit와 clearBit에서 이용한 방법을 섞어서 구현.  

```
int updateBit(int num, int i, int v) {
		int mask = ~(1 << i);
		return (num & mask) | (v << i);
	
```
   
_ _ _
   
[관련문제](https://leetcode.com/tag/bit-manipulation/)  
  
   