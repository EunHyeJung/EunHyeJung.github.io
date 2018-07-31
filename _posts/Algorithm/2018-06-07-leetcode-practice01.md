---
layout: post
title:  "leetcode-practice01"
date:   2018-06-07
author: EunHye Jung
categories: algorithm
tags:	algorithm string two pointers leetcode java
cover:  "/assets/instacode.png"
---

## Valid Palindrome (String)

[https://leetcode.com/problems/valid-palindrome/description/
][leetcode]

문자열이 주어졌을때, 팰린드롬인지 아닌지를 구별하는 프로그램 작성,
문자열에서 영숫자(alphanumeric)만 고려하고 나머지는 무시할것.

Note : 빈문자열(empty string)도 팰린드롬으로 간주.





#### Solution
팰린드롬(palindrome)은 앞으로 읽으나 뒤로 읽으나 같은 문장이나 낱말을 뜻한다.
문자열이 주어졌을때, 앞쪽에서 진행되는 포인터와 뒤쪽에서 진행되는 포인터를 가지고 영숫자(alphanumeric)가 나올때까지 앞쪽포인터(left Pointer)를 뒤로 향하게 하고, 뒤쪽포인터(right pointer)를 앞으로 향하게 한다.
그리고 두개의 포인터가 영숫자라면 동일한 문자열인지를 확인해주면 된다.
각각의 포인터의 범위 체크에 주의가 필요함.

```
	public boolean isPalindrome(String s) {
		s = s.toLowerCase();
		int n = s.length() - 1;
		int lPointer = 0;
		int rPointer = n;

		while (lPointer < rPointer) {
			while (lPointer < n && (!Character.isLetterOrDigit(s.charAt(lPointer)))) {
				lPointer++;
			}
			while (rPointer >= 0 && (!Character.isLetterOrDigit(s.charAt(rPointer)))) {
				rPointer--;
			}

			if (lPointer < rPointer && s.charAt(lPointer) != s.charAt(rPointer)) {
				return false;
			}

			lPointer++;
			rPointer--;
		}

		return true;
	}
```

[leetcode]:   https://leetcode.com/problems/valid-palindrome/description/
