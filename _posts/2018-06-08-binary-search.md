---
layout: post
title:  "Binary Search"
date:   2018-06-07
author: EunHye Jung
categories: algorithm
tags:	Algorithm BinarySearch Java
cover:  "/assets/instacode.png"
---

## Binary Search (이진검색)

[https://leetcode.com/problems/search-insert-position/description/
][binarysearch definition] 

### 이진 검색이란 무엇인가 ?
이진 검색은 컴퓨터공학에서 가장 기본적이고 유용한 알고리즘중 하나이다.
순서가 있는 콜렉션에서 구체적인 값을 찾는 목적으로 사용된다.

이진검색에서 사용되는 용어 :
· Target - 탐색값
· Index - 검색중인 현재위치
· Left, Right - 검색 공간?을 유지하기 위해 사용하는 표식
· Mid - 왼쪽 또는 오른쪽으로 검색해야하는지 결정하기 위한 조건을 적용할 때 사용되는 색인




### 어떻게 이진검색을 식별할까?
이진검색은 매 비교후에  2개의 검색공간으로 나눠진다. 이진탐색은 콜렉션에서 색인 또는 요소를 찾을 필요가 있을때마다 고려된다. 만약 컬렉션이 정렬되지 않은 상태라면, 이진 탐색을 하기전에 먼저 정렬을 해야만한다.




#### 성공적인 이진탐색의 3파트
**1. 전처리** - 컬렉션을 정렬한다.
**2. 이진탐색** - 비교(탐색)후에 반복문이나 재귀를 사용하여 검색공간을 분리한다.
**3. 후처리** - 남은공간에서 탐색가능한 후보자들을 결정




#### 이진탐색을 위한 3템플릿

**Template#1** 

{% highlight javascript %}
	public int binarySearch(int[] nums, int target) {
		if (nums == null || nums.length == 0) {
			return -1;
		}

		int left = 0, right = nums.length - 1;

		while (left <= right) {
			int mid = left + (right - left) / 2;
			if (nums[mid] == target) {
				return mid;
			} else if (nums[mid] < target) {
				left = mid + 1;
			} else {
				right = mid - 1;
			}
		}

		return -1;
	}
{% endhighlight %}


Template #1는 가장 기본적인 이진탐색의 형태이다.



**Template#2** 

{% highlight javascript %}
{% endhighlight %}





[binarysearch definition]:   https://leetcode.com/explore/learn/card/binary-search/